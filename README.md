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
static void GetUserInput()
        {
            int choice;
            ShowMenu();
            bool valid;
            while (true)
            {
                valid = TryGetUserInput("Please enter your choice", out choice);
                if (!valid)
                    ShowMenu();
                else
                {
                    if (choice == (int)Choices.Exit)
                        Environment.Exit(0);
                    HandleUserChoice(choice);
                }
            }
        }

        static bool TryGetUserInput(string message, out int choice)
        {
            Console.WriteLine(message);
            choice = 0;
            try
            {
                if (!int.TryParse(Console.ReadLine(), out choice))
                    throw new FormatException("Choice should be an integer value");
                else if (choice < 0 || choice > 7)
                {
                    Console.WriteLine("InCorrect choice");
                    return false;
                }
                return true;
            }
            catch (FormatException ex)
            {
                Console.WriteLine(ex.Message);
                return false;
            }
        }


        static int GetLength()
        {
            int length = 0;
            bool valid = TryGetLength("Please enter the Length", out length);
            while (!valid)
            {
                valid = TryGetLength("Please enter the Length", out length);
            }
            return length;
        }
        static bool TryGetLength(string message, out int length)
        {
            Console.WriteLine(message);
            length = 0;
            try
            {
                if (!int.TryParse(Console.ReadLine(), out length))
                    throw new FormatException("Length should be an integer value");
                else if (length < 0)
                {
                    Console.WriteLine("Length should be greater than 0");
                    return false;
                }
                return true;
            }
            catch (FormatException ex)
            {
                Console.WriteLine(ex.Message);
                return false;
            }
        }

        static int GetWidth()
        {
            int width = 0;
            bool valid = TryGetWidth("Please enter the Width", out width);
            while (!valid)
            {
                valid = TryGetWidth("Please enter the Width", out width);
            }
            return width;
        }
        static bool TryGetWidth(string message, out int width)
        {
            Console.WriteLine(message);
            width = 0;
            try
            {
                if (!int.TryParse(Console.ReadLine(), out width))
                    throw new FormatException("Width should be an integer value");
                else if (width < 0)
                {
                    Console.WriteLine("Width should be greater than 0");
                    return false;
                }
                return true;
            }
            catch (FormatException ex)
            {
                Console.WriteLine(ex.Message);
                return false;
            }
        }
        
        static void ShowMenu()
        {
            Console.WriteLine("1 = Get Rectangle Length");
            Console.WriteLine("2 = Change Rectangle Length");
            Console.WriteLine("3 = Get Rectangle Width");
            Console.WriteLine("4 = Change Rectangle Width");
            Console.WriteLine("5 = Get Rectangle Perimeter");
            Console.WriteLine("6 = Get Rectangle Area");
            Console.WriteLine("7 = Exit");
            Console.WriteLine(" ");
        }
    }
}


Assignment 02

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Assignment_2
{

    public enum Choices
    {
        TriangleDimensions = 1,
        Exit = 2
    }

    class Program
    {
        static void Main(string[] args)
        {
            GetUserInput();
        }
        
        static void GetUserInput()
        {
            int choice;
            ShowMenu();
            bool valid;
            while (true)
            {
                valid = TryGetUserInput("Please enter your choice!", out choice);
                if (!valid)
                    ShowMenu();
                else
                {
                    if (choice == (int)Choices.Exit)
                        Environment.Exit(0);
                    HandleUserChoice(choice);
                }
            }
        }

        static void HandleUserChoice(int choice)
        {
            switch (choice)
            {
                case (int)Choices.TriangleDimensions:
                    int length = GetLength();
                    int breadth = GetBreadth();
                    int height = GetHeight();
                    Console.WriteLine(TriangleSolver.Analyze(length, breadth, height));
                    break;
            }
        }
        static bool TryGetUserInput(string message, out int choice)
        {
            Console.WriteLine(message);
            choice = 0;
            try
            {
                if (!int.TryParse(Console.ReadLine(), out choice))
                    throw new FormatException("Choice should be an integer value!");
                else if (choice < 0 || choice > 2)
                {
                    Console.WriteLine("InCorrect choice!");
                    return false;
                }
                return true;
            }
            catch (FormatException ex)
            {
                Console.WriteLine(ex.Message);
                return false;
            }
        }
        static void ShowMenu()
        {
            Console.WriteLine("1. Enter triangle dimensions!");
            Console.WriteLine("2. = Exit");
            Console.WriteLine(" ");
        }

        static int GetLength()
        {
            int length = 0;
            bool valid = TryGetLength("Please enter the Length:", out length);
            while (!valid)
            {
                valid = TryGetLength("Please enter the Length:", out length);
            }
            return length;
        }
        static bool TryGetLength(string message, out int length)
        {
            Console.WriteLine(message);
            length = 0;
            try
            {
                if (!int.TryParse(Console.ReadLine(), out length))
                    throw new FormatException("Length should be an integer value!");
                else if (length < 0)
                {
                    Console.WriteLine("Length should be greater than 0!");
                    return false;
                }
                return true;
            }
            catch (FormatException ex)
            {
                Console.WriteLine(ex.Message);
                return false;
            }
        }
        
        static int GetBreadth()
        {
            int breadth = 0;
            bool valid = TryGetBreadth("Please enter the Breadth:", out breadth);
            while (!valid)
            {
                valid = TryGetBreadth("Please enter the Breadth:", out breadth);
            }
            return breadth;
        }
        static bool TryGetBreadth(string message, out int breadth)
        {
            Console.WriteLine(message);
            breadth = 0;
            try
            {
                if (!int.TryParse(Console.ReadLine(), out breadth))
                    throw new FormatException("Breadth should be an integer value!");
                else if (breadth < 0)
                {
                    Console.WriteLine("Breadth should be greater than 0!");
                    return false;
                }
                return true;
            }
            catch (FormatException ex)
            {
                Console.WriteLine(ex.Message);
                return false;
            }
        }

        static int GetHeight()
        {
            int height = 0;
            bool valid = TryGetHeight("Please enter the height:", out height);
            while (!valid)
            {
                valid = TryGetBreadth("Please enter the height:", out height);
            }
            return height;
        }
        static bool TryGetHeight(string message, out int height)
        {
            Console.WriteLine(message);
            height = 0;
            try
            {
                if (!int.TryParse(Console.ReadLine(), out height))
                    throw new FormatException("Height should be an integer value");
                else if (height < 0)
                {
                    Console.WriteLine("Height should be greater than 0");
                    return false;
                }
                return true;
            }
            catch (FormatException ex)
            {
                Console.WriteLine(ex.Message);
                return false;
            }
        }
    }
}

