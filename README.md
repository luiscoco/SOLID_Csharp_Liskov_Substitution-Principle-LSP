# SOLID_Csharp_Liskov_Substitution-Principle-LSP

## Liskov Substitution Principle (LSP):
This principle emphasizes that objects of a derived class should be able to replace objects of the base class without affecting the correctness of the program. 
In other words, a subclass should be substitutable for its base class without causing unexpected behavior.

```csharp
﻿using System;
using System.Security.Cryptography;
using static System.Console;

namespace DotNetDesignPatternDemos.SOLID.LSP;

// using a classic example
public class Rectangle
{
  //public int Width { get; set; }
  //public int Height { get; set; }

  public virtual int Width { get; set; }
  public virtual int Height { get; set; }

  public Rectangle() {}

  public Rectangle(int width, int height)
  {
    Width = width;
    Height = height;
  }

  public bool IsSquare => Width == Height;

  public int Area => Width * Height;

  public override string ToString()
  {
    return $"{nameof(Width)}: {Width}, {nameof(Height)}: {Height}";
  }
}

public class Square : Rectangle
{
  public Square()
  {
  }

  public Square(int side)
  {
    Width = Height = side;
  }

  //public new int Width
  //{
  //  set
  //  {
  //    base.Width = base.Height = value;
  //  }
  //}

  //public new int Height
  //{
  //  set { base.Width = base.Height = value; }
  //}

  public override int Width // nasty side effects
  {
    set => base.Width = base.Height = value;
  }

  public override int Height
  {
    set => base.Width = base.Height = value;
  }
}

public class Demo
{
  public static void UseIt(Rectangle r)
  {
    int width = r.Width;
    r.Height = 10;
    WriteLine($"Expected area of {10*width}, got {r.Area}");
  }

  static void Main()
  {
    var rc = new Rectangle(2,3);
    UseIt(rc);

    var sq = new Square(5);
    UseIt(sq);
  }
}
```


