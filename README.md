Структура проекта:
GeometryLibrary: основная библиотека
IShape: интерфейс для всех фигур
Circle: класс для круга
Triangle: класс для треугольника
GeometryLibrary.Tests: проект с юнит-тестами
Тесты для Circle
Тесты для Triangle
Описание кода:
Интерфейс IShape:

csharp
Копировать код
public interface IShape
{
    double CalculateArea();
}
Класс Circle:

csharp
Копировать код
public class Circle : IShape
{
    public double Radius { get; }

    public Circle(double radius)
    {
        Radius = radius;
    }

    public double CalculateArea()
    {
        return Math.PI * Math.Pow(Radius, 2);
    }
}
Класс Triangle:

csharp
Копировать код
public class Triangle : IShape
{
    public double SideA { get; }
    public double SideB { get; }
    public double SideC { get; }

    public Triangle(double sideA, double sideB, double sideC)
    {
        SideA = sideA;
        SideB = sideB;
        SideC = sideC;
    }

    public double CalculateArea()
    {
        double s = (SideA + SideB + SideC) / 2;
        return Math.Sqrt(s * (s - SideA) * (s - SideB) * (s - SideC));
    }

    public bool IsRightAngled()
    {
        double[] sides = { SideA, SideB, SideC };
        Array.Sort(sides);
        return Math.Abs(Math.Pow(sides[0], 2) + Math.Pow(sides[1], 2) - Math.Pow(sides[2], 2)) < 1e-10;
    }
}
Юнит-тесты:

csharp
Копировать код
[TestClass]
public class GeometryTests
{
    [TestMethod]
    public void CircleAreaTest()
    {
        Circle circle = new Circle(5);
        Assert.AreEqual(Math.PI * 25, circle.CalculateArea(), 1e-10);
    }

    [TestMethod]
    public void TriangleAreaTest()
    {
        Triangle triangle = new Triangle(3, 4, 5);
        Assert.AreEqual(6, triangle.CalculateArea(), 1e-10);
    }

    [TestMethod]
    public void TriangleIsRightAngledTest()
    {
        Triangle triangle = new Triangle(3, 4, 5);
        Assert.IsTrue(triangle.IsRightAngled());
    }
}
