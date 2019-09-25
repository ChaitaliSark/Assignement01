# Assignement01
Software testing methodologies
using System;

namespace Assignment01
{

        public enum Choices
    {
        GetRectangleLength = 1,
        ChangeRectangleLength = 2,
        GetRectangleWidth = 3,
        ChangeRectangleWidth = 4,
        GetRectanglePerimeter = 5,
        GetRectangleArea = 6,
        Exit = 7
    }
    class Program
    {
        static Rectangle rectangle;
        static int length, width;
        static void Main(string[] args)
        {
            rectangle = new Rectangle(); 
            length = GetLength();
            width = GetWidth();
            rectangle = new Rectangle(length, width);
            GetUserInput();
        }

        static void HandleUserChoice(int choice)
        {
            switch (choice)
            {
                case (int)Choices.GetRectangleLength:
                    Console.WriteLine("Length {0}", rectangle.GetLength());
                    break;
                case (int)Choices.ChangeRectangleLength:
                    length = GetLength();
                    Console.WriteLine("Set Length {0}", rectangle.SetLength(length));
                    break;
                case (int)Choices.GetRectangleWidth:
                    Console.WriteLine("Width {0}", rectangle.GetWidth());
                    break;
                case (int)Choices.ChangeRectangleWidth:
                    width = GetWidth();
                    Console.WriteLine("Set Width {0}", rectangle.SetWidth(width));
                    break;
                case (int)Choices.GetRectanglePerimeter:
                    Console.WriteLine("Perimeter {0}", rectangle.GetPerimeter());
                    break;
                case (int)Choices.GetRectangleArea:
                    Console.WriteLine("Area {0}", rectangle.GetArea());
                    break;

            }
        }
