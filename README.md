Assignment 3

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AwesomeCalculator
{
    class Program

    {
        public static int ValidateMenuSelection()
        {
            string userInput = "";
            bool validMenuSelect = false;

            while (validMenuSelect == false)
            {
                Console.WriteLine("1 = Get First Number");
                Console.WriteLine("2 = Change First Number");
                Console.WriteLine("3 = Get Second Number");
                Console.WriteLine("4 = Change Second Number");
                Console.WriteLine("5 = Perform Addition");
                Console.WriteLine("6 = Perform Subtraction");
                Console.WriteLine("7 = Perform Multiplication");
                Console.WriteLine("8 = Perform Division");
                Console.WriteLine("9 = Exit\n");

                Console.WriteLine("Please select an option, by entering a number:\n");
                userInput = Console.ReadLine();

                if (userInput != "1" &&
                    userInput != "2" &&
                    userInput != "3" &&
                    userInput != "4" &&
                    userInput != "5" &&
                    userInput != "6" &&
                    userInput != "7" &&
                    userInput != "8" &&
                    userInput != "9")
                {
                    Console.WriteLine("That's not a valid menu option, please try again:\n");
                }
                else
                {
                    validMenuSelect = true;
                }
            }

            Console.WriteLine();
            return int.Parse(userInput);
        }

        public static double ValidateUserInput(string chosenNumber)
        {
            double aNumber = 1;
            bool isValid = false;

            while (isValid == false)
            {
                Console.WriteLine($"Please enter the {chosenNumber}:");
                string userInput = Console.ReadLine();
                Console.WriteLine();

                bool result = double.TryParse(userInput, out aNumber);

                if (result == false)
                {
                    Console.WriteLine("That's not a valid input please, please try again.\n");
                }

                else
                {
                    isValid = true;
                    Console.WriteLine($"Your {chosenNumber} has been changed to: {aNumber}.\n");
                }
            }

            return aNumber;
        }


        static void Main(string[] args)
        {
            Calc c = new Calc();
            bool validCalcSelect = false;
            string calcSelection;
            int selection;

            while (validCalcSelect == false)
            {
                Console.WriteLine("1 = Use random numbers between 0 and 501 for your calculation\n");
                Console.WriteLine("2 = Provide your own numbers\n");
                Console.WriteLine("Choose a menu item to begin:");
                calcSelection = Console.ReadLine();
                Console.WriteLine();

                if (calcSelection != "1" && calcSelection != "2")
                {
                    Console.WriteLine("That's not a valid selection, please try again.\n");
                }
                else if (int.Parse(calcSelection) == 1)
                {
                    validCalcSelect = true;
                    Random random = new Random();
                    double firstNumber;
                    double secondNumber;

                    firstNumber = Math.Round((random.NextDouble() * 500), 2);
                    secondNumber = Math.Round((random.NextDouble() * 500), 2);

                    Console.WriteLine($"Your random numbers are {firstNumber} and {secondNumber}.\n");
                    Calc customCalc = new Calc(firstNumber, secondNumber);
                    c = customCalc;

                }
                else if (int.Parse(calcSelection) == 2)
                {
                    validCalcSelect = true;

                    double firstNumber;
                    double secondNumber;

                    firstNumber = ValidateUserInput("firstNumber");
                    secondNumber = ValidateUserInput("secondNumber");

                    Console.WriteLine($"Your custom numbers are {firstNumber} and {secondNumber}.\n");
                    Calc customCalc = new Calc(firstNumber, secondNumber);
                    c = customCalc;
                }
            }


            selection = ValidateMenuSelection();

            while (selection != 9)
            {
                double result;

                switch (selection)
                {
                    case 1:
                        Console.WriteLine($"First Number is: {c.GetFirstNumber()}\n");
                        break;
                    case 2:
                        result = ValidateUserInput("firstNumber");
                        c.SetFirstNumber(result);
                        break;
                    case 3:
                        Console.WriteLine($"Second Number is: {c.GetSecondNumber()}\n");
                        break;
                    case 4:
                        result = ValidateUserInput("secondNumber");
                        c.SetSecondNumber(result);
                        break;
                    case 5:
                        Console.WriteLine($"The result of {c.GetFirstNumber()} + {c.GetSecondNumber()} is: {c.GetAddition()}\n");
                        break;
                    case 6:
                        Console.WriteLine($"The result of {c.GetFirstNumber()} - {c.GetSecondNumber()} is: {c.GetSubtraction()}\n");
                        break;
                    case 7:
                        Console.WriteLine($"The result of {c.GetFirstNumber()} * {c.GetSecondNumber()} is: {c.GetMultiplication()}\n");
                        break;
                    case 8:
                        Console.WriteLine($"The result of {c.GetFirstNumber()} / {c.GetSecondNumber()} is: {c.GetDivision()}\n");
                        break;
                    default:
                        break;
                }

                selection = ValidateMenuSelection();

            }

        }
    }
}


Assignment#3 Test Cases:

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using AwesomeCalculator;
using NUnit.Framework;


namespace AwesomeCalculatorTest
{
    [TestFixture]
    public class Class1
    {

        [Test]
        public void GetAddition_Input3point4and5point6_Returns9point0()
        {
            double num1 = 3.4;
            double num2 = 5.6;

            double result = num1 + num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetAddition(); // Act
            Assert.AreEqual(result, actualResult);

        }

        [Test]

        public void GetAddition_Input10point0and2point0_Returns12point0()
        {
            double num1 = 10.0;
            double num2 = 2.0;

            double result = num1 + num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetAddition(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetAddition_Input2point0and3point0_Returns5point0()
        {
            double num1 = 2.0;
            double num2 = 3.0;

            double result = num1 + num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetAddition(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetAddition_Input7point4and3point6_Returns11point0() {
            double num1 = 7.4;
            double num2 = 3.6;

            double result = num1 + num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetAddition(); // Act
            Assert.AreEqual(result, actualResult);
        }


        [Test]

        public void GetMultiplication_Input5point0and2point0_Returns10point0()
        {
            double num1 = 5.0;
            double num2 = 2.0;

            double result = num1 * num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetMultiplication(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetMultiplication_Input6point0and2point0_Returns12point0()
        {
            double num1 = 6.0;
            double num2 = 2.0;

            double result = num1 * num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetMultiplication(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetMultiplication_Input4point0and2point0_Returns8point0()
        {
            double num1 = 4.0;
            double num2 = 2.0;

            double result = num1 * num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetMultiplication(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetMultiplication_Input10point0and2point0_Returns20point0()
        {
            double num1 = 10.0;
            double num2 = 2.0;

            double result = num1 * num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetMultiplication(); // Act
            Assert.AreEqual(result, actualResult);
        }





                [Test]

        public void GetSubtraction_Input4point0and1point0_Returns3point0()
        {
            double num1 = 4.0;
            double num2 = 1.0;

            double result = num1 - num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetSubtraction(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetSubtraction_Input5point9and1point9_Returns4point0()
        {
            double num1 = 5.9;
            double num2 = 1.9;

            double result = num1 - num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetSubtraction(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetSubtraction_Input15point0and7point0_Returns8point0()
        {
            double num1 = 15.0;
            double num2 = 7.0;

            double result = num1 - num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetSubtraction(); // Act
            Assert.AreEqual(result, actualResult);
        }




        [Test]

        public void GetDivision_Input7point0and3point5_Returns2point0()
        {
            double num1 = 7.0;
            double num2 = 3.5;

            double result = num1 / num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetDivision(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetDivision_Input5point0and2point5_Returns2point0()
        {
            double num1 = 5.0;
            double num2 = 2.5;

            double result = num1 / num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetDivision(); // Act
            Assert.AreEqual(result, actualResult);
        }

        [Test]

        public void GetDivision_Input14point2and2point2_Returns7point0()
        {
            double num1 = 14.0;
            double num2 = 2.0;

            double result = num1 / num2;
            Calc testCalc = new Calc(num1, num2); // Arrange
            double actualResult = testCalc.GetDivision(); // Act
            Assert.AreEqual(result, actualResult);
        }

    }
}
