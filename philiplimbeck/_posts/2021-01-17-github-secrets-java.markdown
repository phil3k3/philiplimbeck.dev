---
layout: single 
title:  "Creating GitHub Secrets programmatically"
date:   2021-02-19 16:11:35 +0200
classes: wide
---

GitHub Actions offer an easy and straightfoward way to setup Workflows around your repository to run tests, build your
service and even push it to a registry. GitHub itself offers a variety of templates to chose from to deploy your
application to a selection of cloud providers (i.e. AWS, Google Cloud) or run tests using test frameworks for all
popular languages.

This sounds like a great feature by itself if you ignore security for a while. If you don't you will soon realize that
you need to your passwords, access keys or JWT tokens to deploy to your cluster or access your docker registry
somewhere.

GitHub provides a solution for that as well with so called 'Secrets'. Secrets can be tied to your GitHub organization or
your repository only and provide a secure way to have them at hand for the workflow when necesary.

You can manually define these secrets on the settings page for both the repository and the organization:

![action_secrets](/assets/images/github_action_secrets.png)

But what if you want to set these up programmatically? In this case you have to generate the secret yourself.

The first step involves fetching your keyId and encryption key from the GitHub repository where you want to create the
secret:

```java
private static Pair<String,String> getEncryptionKey(String authToken,OkHttpClient client,String repository) throws IOException {
    Request request = new Request.Builder()
        .url(String.format("https://api.github.com/repos/%s/actions/secrets/public-key",repository))
        .addHeader("Authorization","token "+token)
        .build();
    try(Response response=client.newCall(request).execute()) {
        JsonObject jsonObject = JsonParser.parseString(response.body().string()).getAsJsonObject();
        return Pair.of(jsonObject.get("key_id").getAsString(), jsonObject.get("key").getAsString());
    }
}
```

After this, you can use the encryption key and the key id to generate and create or update the secret in GitHub. 

```java
 // the GitHub repository in the form <organization>/<repository>
String repository = "...";
Pair<String,String> encryptionKeyIdAndValue = getEncryptionKey(authToken, client, repository);

// Auth token is the authentication token for your GitHub repository
String authToken = "...";
        
String secretKey = "mySecretKey";
String secretValue = "mySecretValue";

LazySodiumJava lazySodium = new LazySodiumJava(new SodiumJava());

Box.Lazy lazy = (Box.Lazy) lazySodium;
Helpers.Lazy helpers = (Helpers.Lazy) lazySodium;

// base64 decode encryption key
byte[] encryptionKey = Base64.decode(encryptionKeyIdAndValue.right);

// encrypt secret value using encryption key
String secretEncrypted = lazy.cryptoBoxSealEasy(secretValue, Key.fromBytes(encryptionKey));

// cryptoBoxSealEasy returns encrypted secret in hex representation, convert to a binary representation first...
byte[] secretByteArray = helpers.sodiumHex2Bin(secretEncrypted);

//...and then use base64 encoding to prepare it for the PUT request
String secretEncryptedBin = new String(Base64.encode(secretByteArray), StandardCharsets.UTF_8);

String payload = String.format("{\"key_id\": \"%s\", \"encrypted_value\": \"%s\"}", encryptionKeyIdAndValue.left, secretEncryptedBin);
        
Request request = new Request.Builder()
        .url("https://api.github.com/repos/nicekube/deployable-service/actions/secrets/"+secretKey)
        .addHeader("Authorization", "token " + token)
        .put(RequestBody.create(payload, MediaType.get("application/vnd.github.v3+json")))
        .build();

OkHttpClient client = new OkHttpClient();
client.newCall(request).execute()
```

This is how you create or update a GitHub secret programmatically.


