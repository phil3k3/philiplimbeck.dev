---
title:  "Using ByteBuddy to generate classes at runtime"
date:   2021-01-01 16:11:35 +0200
featured_image: '/images/demo/bytebuddy.png'
---

Although the JDK offers a reflection capabiliies which allow you to introspect classes, their methods and properties,
sometimes it is not enough as all of these capabilites assume a static definition of classes which are cemented during
compile time. That means that you cannot define the class once it has been compiled and loaded by the class loader.

In some scenarios, what you actually want is to generate a class at runtime depending on your needs and have it picked up by
other frameworks or libraries. There are many out there but today we want to take a look at ByteBuddy.

https://bytebuddy.net/#/ is a framework which allows to generate classes dynamically, This means you can create a class,
add methods to which you can use to delegate it to your own objects, define annotations and many things more.

Let's look at a simple example:

```java

class MyClass {
    public String originalMethod() {
        return "original method called";
    }
}

class Test {
    public static void main(String[] args){
        Class<?> dynamicType = new ByteBuddy()
          .subclass(MyClass.class)
          .method(ElementMatchers.named("originalMethod"))
          .intercept(FixedValue.value("overriden method called"))
          .make()
          .load(getClass().getClassLoader())
          .getLoaded();
        MyClass myClass = (MyClass)dynamicType.getDeclaredConstructor().newInstance();
        System.out.println(myClass.originalMethod());
    }
}
```
The snipped above will print the content of the overridden method instead of the original method.
