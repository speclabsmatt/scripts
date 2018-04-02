# scripts

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace calculator
{
    class Program
    {
        static void Main(string[] args)
        {
            //Create UI object and start
            UserInterface ui = new UserInterface();
            ui.Start();
        }
    }
}

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace calculator
{
    public class UserInterface
    {
        private Calculator calc; 

        public UserInterface()
        {
            //Initialize caluclator for operations
            this.calc = new Calculator();
        }

        //Print greeting and menu
        public void Start()
        {
            this.PrintGreeting();
            this.PrintMenu();
        }

        //Output greeting
        public void PrintGreeting()
        {
            Console.WriteLine("Welcome to the Paycom C# Calculator \n" +
                "Written by Matthew C. Lanier \n" +
                "------------------------------------ \n" +
                "Type :q and press enter to quit at any time. \n" +
                "You can also type :m and press enter to return to the menu any time within the program.");
        }

        //Output menu and get user selection
        public void PrintMenu()
        {
            Console.WriteLine("------------------------------------ \n" +
                "MAIN MENU \n" +
                "Please choose an operation from the menu by entering the number and pressing enter. \n" +
                "1  -  Addition \n" +
                "2  -  Subtraction \n" +
                "3  -  Multiplication \n" +
                "4  -  Division");
            Console.Write("Enter selection> ");
            this.ParseMenuInput(Console.ReadLine());
        }

        public void ParseMenuInput(String input)
        {
            CheckForStaticOperation(input.Trim()); //check for :q or :m

            if (input.Trim().Equals("1"))
            {
                Console.WriteLine("Addition selected.");
                Console.Write("Enter first number> ");

                var numOne = Console.ReadLine();
                var parsedOne = ParseNum(numOne);

                Console.Write("Enter second number> ");

                var numTwo = Console.ReadLine();
                var parsedTwo = ParseNum(numTwo);
                Console.WriteLine(calc.Sum(parsedOne, parsedTwo));
            }
            else if (input.Trim().Equals("2"))
            {

            }
            else if (input.Trim().Equals("3"))
            {

            }
            else if (input.Trim().Equals("4"))
            {

            }
            else
            {
                Console.WriteLine("Invalid operation selected. Please try again.");
                this.PrintMenu();
            }
        }

        public void CheckForStaticOperation(String input)
        {
            if (input.Equals(":q"))
            {
                Console.WriteLine("Exiting application.");
                Environment.Exit(0);
            }
            else if (input.Equals(":m"))
            {
                this.PrintMenu();
            }
        }

        public object ParseNum(String num)
        {
            if (int.TryParse(num, out int intNbr))
            {
                return intNbr;
            }
            else if (Single.TryParse(num, out float fltNbr))
            {
                return fltNbr;
            }
            else
            {
                return false;
            }
        }
    }
}



using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace calculator
{
    public class Calculator
    {
        public Calculator()
        {
        }

        public T Sum<T>(T value1, T value2)
        {
            dynamic temp = value1;
            temp += value2;
            return temp;
        }
    }
}
