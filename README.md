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






CREATE DATABASE training;

CREATE TABLE parents (
	parentid MEDIUMINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(30) NOT NULL,
	PRIMARY KEY (parentid)
);

CREATE TABLE children {
	childid MEDIUMINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(30) NOT NULL,
	parentid MEDIUMINT,
	PRIMARY KEY (childid),
	FOREIGN KEY (parentid) REFERENCES parents(parentid)
);

INSERT INTO parents (name) VALUES
	('John'),
	('Mark'), 
	('Sarah'), 
	('Daniel'),
	('Jamie');

INSERT INTO children (name, parentid) VALUES
	('Mary', (SELECT parentid FROM parents WHERE name = 'John' LIMIT 1) ),
	('Jake', (SELECT parentid FROM parents WHERE name = 'Mark' LIMIT 1) ),
	('Gary', (SELECT parentid FROM parents WHERE name = 'Sarah' LIMIT 1) ),
	('Tim', (SELECT parentid FROM parents WHERE name = 'Daniel' LIMIT 1) ),
	('Debbie', (SELECT parentid FROM parents WHERE name = 'Jamie' LIMIT 1) );

---------------

CREATE DATABASE nfl;

CREATE TABLE teams (
	teamid MEDIUMINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(30) NOT NULL,
	PRIMARY KEY (teamid)
);

CREATE TABLE players (
	playerid MEDIUMINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(30) NOT NULL,
	teamid MEDIUMINT,
	PRIMARY KEY (playerid),
	FOREIGN KEY (teamid) REFERENCES teams(teamid)
	ON DELETE CASCADE
);

INSERT INTO teams (name) VALUES
	('Cowboys'),
	('Patriots'), 
	('Eagles');

INSERT INTO players (name, teamid) VALUES
	('Dez Bryant', (SELECT teamid FROM teams WHERE name = 'Cowboys' LIMIT 1) ),
	('Dak Prescott', (SELECT parentid FROM parent WHERE name = 'Cowboys' LIMIT 1) ),
	('Ezekiel Elliott', (SELECT parentid FROM parent WHERE name = 'Cowboys' LIMIT 1) ),
	('Allen Hurns', (SELECT parentid FROM parent WHERE name = 'Cowboys' LIMIT 1) ),
	('Jason Witten', (SELECT parentid FROM parent WHERE name = 'Cowboys' LIMIT 1) ),
	('Tom Brady', (SELECT teamid FROM teams WHERE name = 'Patriots' LIMIT 1) ),
	('Rob Gronkowski', (SELECT parentid FROM parent WHERE name = 'Patriots' LIMIT 1) ),
	('Danny Amendola', (SELECT parentid FROM parent WHERE name = 'Patriots' LIMIT 1) ),
	('Julian Edelman', (SELECT parentid FROM parent WHERE name = 'Patriots' LIMIT 1) ),
	('Dion Lewis', (SELECT parentid FROM parent WHERE name = 'Patriots' LIMIT 1) ),
	('Carson Wentz', (SELECT teamid FROM teams WHERE name = 'Eagles' LIMIT 1) ),
	('Nick Foles', (SELECT parentid FROM parent WHERE name = 'Eagles' LIMIT 1) ),
	('Michael Bennett', (SELECT parentid FROM parent WHERE name = 'Eagles' LIMIT 1) ),
	('Chris Long', (SELECT parentid FROM parent WHERE name = 'Eagles' LIMIT 1) ),
	('Zach Ertz', (SELECT parentid FROM parent WHERE name = 'Eagles' LIMIT 1) );

UPDATE players SET name = 'John Smith';

DELETE FROM team WHERE name = 'Cowboys';

---------------

CREATE DATABASE nba;

CREATE TABLE cities (
	cityid MEDIUMINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(30) NOT NULL,
	PRIMARY KEY (cityid)
);

CREATE TABLE teams (
	teamid MEDIUMINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(30) NOT NULL,
	cityid MEDIUMINT,
	PRIMARY KEY (teamid),
	FOREIGN KEY (cityid) REFERENCES cities(cityid)
	ON DELETE CASCADE
);

CREATE TABLE players (
	playerid MEDIUMINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(30) NOT NULL,
	teamid MEDIUMINT,
	PRIMARY KEY (playerid),
	FOREIGN KEY (teamid) REFERENCES teams(teamid)
	ON DELETE CASCADE
);


INSERT INTO cities (name) VALUES 
	('LA'), ('Memphis'), ('Miami'), ('Milwaukee'), ('New Orleans'),
	('New York'), ('OKC'), ('Orlando'), ('Philadelphia'), ('Portland');

INSERT INTO teams (name, cityid) VALUES
	('Thunder', (SELECT cityid FROM cities WHERE name = 'OKC' LIMIT 1) ), 
	('Lakers', (SELECT cityid FROM cities WHERE name = 'LA' LIMIT 1) ),
	('Heat', (SELECT cityid FROM cities WHERE name = 'Miami' LIMIT 1) );

INSERT INTO players (name, teamid) VALUES
	('Russell Westbrook', (SELECT teamid FROM teams WHERE name = 'Thunder' LIMIT 1) ),
	('Carmelo Anthony', (SELECT teamid FROM teams WHERE name = 'Thunder' LIMIT 1) ),
	('Paul George', (SELECT teamid FROM teams WHERE name = 'Thunder' LIMIT 1) ),
	('Steven Adams', (SELECT teamid FROM teams WHERE name = 'Thunder' LIMIT 1) ),
	('Andre Roberson', (SELECT teamid FROM teams WHERE name = 'Thunder' LIMIT 1) ),
	('Lonzo Ball', (SELECT teamid FROM teams WHERE name = 'Lakers' LIMIT 1) ),
	('Isaiah Thomas', (SELECT teamid FROM teams WHERE name = 'Lakers' LIMIT 1) ),
	('Brandon Ingram', (SELECT teamid FROM teams WHERE name = 'Lakers' LIMIT 1) ),
	('Kyle Kuzma', (SELECT teamid FROM teams WHERE name = 'Lakers' LIMIT 1) ),
	('Julius Randle', (SELECT teamid FROM teams WHERE name = 'Lakers' LIMIT 1) ),
	('Dwyane Wade', (SELECT teamid FROM teams WHERE name = 'Heat' LIMIT 1) ),
	('Hassan Whiteside', (SELECT teamid FROM teams WHERE name = 'Heat' LIMIT 1) ),
	('Goran Dragic', (SELECT teamid FROM teams WHERE name = 'Heat' LIMIT 1) ),
	('Tyler Johnson', (SELECT teamid FROM teams WHERE name = 'Heat' LIMIT 1) ),
	('James Johnson', (SELECT teamid FROM teams WHERE name = 'Heat' LIMIT 1) );

DELETE FROM teams WHERE name = 'Lakers'; 
