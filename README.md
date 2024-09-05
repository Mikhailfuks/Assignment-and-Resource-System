using System;
using System.Collections.Generic;

public class AssignmentAndResourceSystem
{
    private static Dictionary<string, List<Assignment>> assignmentsByStudent = new Dictionary<string, List<Assignment>>();
    private static Dictionary<string, List<Resource>> resourcesBySubject = new Dictionary<string, List<Resource>>();

    public static void Main(string[] args)
    {
        Console.WriteLine("Welcome to the Assignment and Resource System");

        while (true)
        {
            Console.WriteLine("nChoose an option:");
            Console.WriteLine("1. Add Assignment");
            Console.WriteLine("2. Add Resource");
            Console.WriteLine("3. View Assignments by Student");
            Console.WriteLine("4. View Resources by Subject");
            Console.WriteLine("5. Exit");

            int choice = GetIntInput("Enter your choice: ");

            switch (choice)
            {
                case 1:
                    AddAssignment();
                    break;
                case 2:
                    AddResource();
                    break;
                case 3:
                    ViewAssignmentsByStudent();
                    break;
                case 4:
                    ViewResourcesBySubject();
                    break;
                case 5:
                    Console.WriteLine("Exiting the system. Goodbye!");
                    return;
                default:
                    Console.WriteLine("Invalid choice. Please try again.");
                    break;
            }
        }
    }

    private static void AddAssignment()
    {
        Console.WriteLine("nAdding Assignment");
        Console.Write("Enter student name: ");
        string studentName = Console.ReadLine();
        Console.Write("Enter assignment title: ");
        string assignmentTitle = Console.ReadLine();
        Console.Write("Enter assignment description: ");
        string assignmentDescription = Console.ReadLine();

        Assignment newAssignment = new Assignment(assignmentTitle, assignmentDescription);

        if (assignmentsByStudent.ContainsKey(studentName))
        {
            assignmentsByStudent[studentName].Add(newAssignment);
        }
        else
        {
            assignmentsByStudent[studentName] = new List<Assignment>() { newAssignment };
        }
        Console.WriteLine("Assignment added successfully.");
    }

    private static void AddResource()
    {
        Console.WriteLine("nAdding Resource");
        Console.Write("Enter subject: ");
        string subject = Console.ReadLine();
        Console.Write("Enter resource title: ");
        string resourceTitle = Console.ReadLine();
        Console.Write("Enter resource URL: ");
        string resourceURL = Console.ReadLine();

        Resource newResource = new Resource(resourceTitle, resourceURL);

        if (resourcesBySubject.ContainsKey(subject))
        {
            resourcesBySubject[subject].Add(newResource);
        }
        else
        {
            resourcesBySubject[subject] = new List<Resource>() { newResource };
        }
        Console.WriteLine("Resource added successfully.");
    }

    private static void ViewAssignmentsByStudent()
    {
        Console.WriteLine("nView Assignments by Student");
        Console.Write("Enter student name: ");
        string studentName = Console.ReadLine();

        if (assignmentsByStudent.ContainsKey(studentName))
        {
            Console.WriteLine($"Assignments for {studentName}:");
            foreach (Assignment assignment in assignmentsByStudent[studentName])
            {
                Console.WriteLine($"- {assignment.Title} - {assignment.Description}");
            }
        }
        else
        {
            Console.WriteLine($"No assignments found for {studentName}.");
        }
    }

    private static void ViewResourcesBySubject()
    {
        Console.WriteLine("nView Resources by Subject");
        Console.Write("Enter subject: ");
        string subject = Console.ReadLine();

        if (resourcesBySubject.ContainsKey(subject))
        {
            Console.WriteLine($"Resources for {subject}:");
            foreach (Resource resource in resourcesBySubject[subject])
            {
                Console.WriteLine($"- {resource.Title} - {resource.URL}");
            }
        }
        else
        {
            Console.WriteLine($"No resources found for {subject}.");
        }
    }

    // Helper method to get integer input from the user
    private static int GetIntInput(string prompt)
    {
        while (true)
        {
            Console.Write(prompt);
            if (int.TryParse(Console.ReadLine(), out int input))
            {
                return input;
            }
            Console.WriteLine("Invalid input. Please enter a number.");
        }
    }
}

// Assignment class
public class Assignment
{
    public string Title { get; set; }
    public string Description { get; set; }

    public Assignment(string title, string description)
    {
        Title = title;
        Description = description;
    }
}

// Resource class
public class Resource
{
    public string Title { get; set; }
    public string URL { get; set; }

    public Resource(string title, string url)
    {
        Title = title;
        URL = url;
    }
}
