import java.util.ArrayList;
import java.util.Scanner;
public class StudentGradeTracker 
{
    private ArrayList<String> studentNames;
    private ArrayList<Double> studentGrades;
    private Scanner scanner;
    public StudentGradeTracker() 
    {
        studentNames = new ArrayList<>();
        studentGrades = new ArrayList<>();
        scanner = new Scanner(System.in);
    }
    public void run() 
    {
        System.out.println("*** Student Grade Tracker ***");        
        while (true) 
        {
            displayMenu();
            int choice = scanner.nextInt();
            scanner.nextLine();            
            switch (choice) 
            {
                case 1:
                    addStudent();
                    break;
                case 2:
                    displayAllStudents();
                    break;
                case 3:
                    calculateAverage();
                    break;
                case 4:
                    findHighestScore();
                    break;
                case 5:
                    findLowestScore();
                    break;
                case 6:
                    generateReport();
                    break;
                case 7:
                    System.out.println("Exiting the program...");
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
    private void displayMenu() 
    {
        System.out.println("\nMain Menu:");
        System.out.println("1. Add a student and grade");
        System.out.println("2. View all students");
        System.out.println("3. Calculate average grade");
        System.out.println("4. Find highest score");
        System.out.println("5. Find lowest score");
        System.out.println("6. Generate summary report");
        System.out.println("7. Exit");
        System.out.print("Enter your choice: ");
    }
    private void addStudent() 
    {
        System.out.print("Enter student name: ");
        String name = scanner.nextLine(); 
        System.out.print("Enter student grade (0-100): ");
        double grade = scanner.nextDouble();
        // Validate grade
        if (grade < 0 || grade > 100) 
        {
            System.out.println("Invalid grade. Grade must be between 0 and 100.");
            return;
        }        
        studentNames.add(name);
        studentGrades.add(grade);
        System.out.println("Student added successfully!");
    }
    private void displayAllStudents() 
    {
        if (studentNames.isEmpty()) 
        {
            System.out.println("No students in the system.");
            return;
        }        
        System.out.println("\nList of Students:");
        System.out.println("-----------------");
        for (int i = 0; i < studentNames.size(); i++) 
        {
            System.out.printf("%-20s: %.2f%n", studentNames.get(i), studentGrades.get(i));
        }
    }
    private void calculateAverage() 
    {
        if (studentGrades.isEmpty()) 
        {
            System.out.println("No grades to calculate average.");
            return;
        }        
        double sum = 0;
        for (double grade : studentGrades) 
        {
            sum += grade;
        }        
        double average = sum / studentGrades.size();
        System.out.printf("The average grade is: %.2f%n", average);
    }
    private void findHighestScore() 
    {
        if (studentGrades.isEmpty()) 
        {
            System.out.println("No grades available.");
            return;
        }       
        double highest = studentGrades.get(0);
        int index = 0;        
        for (int i = 1; i < studentGrades.size(); i++) 
        {
            if (studentGrades.get(i) > highest) 
            {
                highest = studentGrades.get(i);
                index = i;
            }
        }        
        System.out.printf("Highest score: %s with %.2f%n", studentNames.get(index), highest);
    }
    private void findLowestScore() 
    {
        if (studentGrades.isEmpty()) 
        {
            System.out.println("No grades available.");
            return;
        }        
        double lowest = studentGrades.get(0);
        int index = 0;        
        for (int i = 1; i < studentGrades.size(); i++) 
        {
            if (studentGrades.get(i) < lowest) 
            {
                lowest = studentGrades.get(i);
                index = i;
            }
        }        
        System.out.printf("Lowest score: %s with %.2f%n", studentNames.get(index), lowest);
    }
    private void generateReport() 
    {
        if (studentGrades.isEmpty()) 
        {
            System.out.println("No data available for report.");
            return;
        }
        System.out.println("\n=== Student Grade Summary Report ===");
        System.out.println("-----------------------------------");       
        // Display all students
        displayAllStudents();        
        // Calculate and display statistics
        calculateAverage();
        findHighestScore();
        findLowestScore();        
        System.out.println("-----------------------------------");
        System.out.println("Total Students: " + studentNames.size());
    }
    public static void main(String[] args) 
    {
        StudentGradeTracker tracker = new StudentGradeTracker();
        tracker.run();
    }
}
