#include <iostream>
#include <string>
#include <vector>
using namespace std;

class College {
public:
    string College_Name;
    string College_Location;

    College(string college_name, string college_location) {
        College_Name = college_name;
        College_Location = college_location;
    }

    void College_Info() {
        cout << "College: " << College_Name << endl;
        cout << "College Location: " << College_Location << endl << endl;
    }
};

class DateOfBirth {
public:
    int Day_of_Birth;
    int Month_of_Birth;
    int Year_of_Birth;

    DateOfBirth(int day_of_birth, int month_of_birth, int year_of_birth) {
        Day_of_Birth = day_of_birth;
        Month_of_Birth = month_of_birth;
        Year_of_Birth = year_of_birth;
    }

    void dob() {
        cout << "Date of Birth: " << Day_of_Birth << "/" << Month_of_Birth << "/" << Year_of_Birth << endl;
    }

    void StudentAge(int Current_date, int Current_month, int Current_year) {
        if (Year_of_Birth > Current_year || Month_of_Birth > 12)
            cout << "Age: Invalid" << endl << endl;
        else if (Year_of_Birth == Current_year && (Day_of_Birth >= Current_date || Month_of_Birth >= Current_month))
            cout << "Age: 0" << endl << endl;
        else if (Year_of_Birth < Current_year && ((Month_of_Birth == Current_month && Day_of_Birth <= Current_date) || Month_of_Birth < Current_month))
            cout << "Age: " << Current_year - Year_of_Birth << endl << endl;
        else if (Year_of_Birth < Current_year && (Month_of_Birth == Current_month && Day_of_Birth > Current_date || Month_of_Birth > Current_month))
            cout << "Age: " << Current_year - Year_of_Birth - 1 << endl << endl;
    }
};

class Student {
private:
    string Course;
    vector<int> Marks;       // Using vector for dynamic array
    double GPA;
    double CGPA;
    string Semester;
    vector<int> CreditUnits; // Using vector for dynamic array

public:
    string Student_Name;
    string Reg_Number;

    Student(string student_name, string reg_number, string semester, string course, vector<int> marks, vector<int> credit_units, double gpa)
        : Student_Name(student_name), Reg_Number(reg_number), Semester(semester), Course(course), Marks(marks), CreditUnits(credit_units), GPA(gpa) {
        CGPA = CalculateGPA();
    }

    void StudentDetails() {
        cout << "Student Name: " << Student_Name << endl;
        cout << "Reg. Number: " << Reg_Number << endl;
        cout << "Course: " << Course << endl;
    }

    void Results() {
        cout << "Marks: ";
        for (int mark : Marks) {
            cout << mark << " ";
        }
        cout << endl;
        cout << "Initial GPA: " << GPA << endl;
        cout << "Current semester GPA: " << GPA << endl;
        cout << "Current semester CGPA: " << CGPA << endl;
    }

    // Function to determine grade points based on marks
    double CalculateGradePoint(int score) {
        if (score >= 80 && score <= 100)
            return 5.0;
        else if (score >= 75)
            return 4.5;
        else if (score >= 70)
            return 4.0;
        else if (score >= 65)
            return 3.5;
        else if (score >= 60)
            return 3.0;
        else if (score >= 55)
            return 2.5;
        else if (score >= 50)
            return 2.0;
        else if (score >= 45)
            return 1.0;
        else if (score >= 40)
            return 0.5;
        else
            return 0.0;
    }

    // Function to calculate GPA based on marks and credit units
    double CalculateGPA() {
        double totalPoints = 0.0;  // Total weighted points
        int totalCredits = 0;       // Total credits

        for (size_t i = 0; i < Marks.size(); ++i) {
            double gradePoint = CalculateGradePoint(Marks[i]);
            totalPoints += gradePoint * CreditUnits[i];  // Weighted points
            totalCredits += CreditUnits[i];                // Total credits
        }

        return (totalCredits > 0) ? (totalPoints / totalCredits) : 0.0;  // Avoid division by zero
    }
};

int main() {
    College college1("CEDAT", "Main Campus");

    // Initialize with marks and credit units as vectors
    Student student1("BALUKU David", "21/U/1065", "Two", "Bsc. Electrical Engineering", {88, 78, 71, 61, 66, 65}, {3, 4, 3, 3, 2, 3}, 4.5);
    DateOfBirth student1_dob(18, 11, 1982);

    cout << "COLLEGE DETAILS:" << endl << endl;
    college1.College_Info();

    cout << "STUDENT BIODATA:" << endl << endl;
    student1.StudentDetails();
    student1_dob.dob();
    student1_dob.StudentAge(7, 10, 2024);
    cout << "RESULTS:" << endl << endl;
    student1.Results();

    return 0;
}
