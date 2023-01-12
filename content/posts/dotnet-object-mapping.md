---
title: ".NET object mapping"
date: 2023-01-12
summary: "Ways to map objects without auto mapper"
---

## Intro

In this post I will try to cover few ways hot to map objects from one to another.
There exists library exactly for this purpose. It is called [AutoMapper](https://github.com/AutoMapper/AutoMapper).
However for smaller objects in smaller projects it might seem unnecessary to use external library.

## Objects

We will use following objects:

```cs
/* Person1.cs */
public class Person1
{
    public string? FirstName { get; set; }
    public string? LastName { get; set; }
    public DateOnly BirthDate { get; set; }
    public int? Height { get; set; }
}

/* Person2.cs */
public class Person2
{
    public string? FullName { get; set; }
    public DateTime BrithDate { get; set; }
    public int? Height { get; set; }
}
```
Let's check each mapping method now.

## Constructors

Most obvious way is to use constructors.

```cs
/* Person2.cs */
public Person2 (Person1 p)
{
    this.FullName = $"{p.FirstName} {p.LastName}";
    this.BirthDate = p.BirthDate.ToDateTime();
    this.Height = p.Height;
}

/* Person1.cs */
public Person1 (Person2 p)
{
    /* ... */
}
```

Then you can create new mapped object like this:

```cs
var person2 = new Person2(person1);
```
- Pros: Very simple; Clean to read  
- Cons: Objects are dependent on each other

## Using implicit and explicit operators

```cs
/* Person2.cs */
public static explicit operator Person2(Person1 p)
{
    this.FullName = $"{p.FirstName} {p.LastName}";
    this.BirthDate = p.BirthDate.ToDateTime();
    this.Height = p.Height;
}

public static implicit operator Person1(Person2 p)
{
    /* ... */
}
```
- Proc: Using native type conversion  
- Cons: At least on object is dependent on other; Not so clean to read due to abstraction  

## Mapping extensions

```cs
/* MappingExtensions.cs */
public static class MappingExtensions
{
    public static Person2 ToPerson2(this Person1 from)
    {
        return new Person2
        {
            FullName = $"{this.FirstName} {this.LastName}";
            BirthDate = this.BirthDate.ToDateTime();
            Height = this.Height;
        };
    }
    
    public static Person1 ToPerson1(this Person2 from)
    {
        /* ... */
    }
}
```

Then mapping itself is very clean to read:

```cs
var person2 = person1.ToPerson2();
```
Pros: Objects are independent on each other; Very clean to read; Mapping is on one place  
Cons: 
