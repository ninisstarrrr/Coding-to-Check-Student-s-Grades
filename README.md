#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

struct Subject {
    string subjectName;
    int credit;
    double mark;
    string grade;
};

struct Student {
    string name;
    int age;
    int numSubjects;
    Subject subjects[5];
    double cpa;
};

string calculateGrade(double mark) {
    if (mark >= 90) return "A+";
    else if (mark >= 85) return "A";
    else if (mark >= 80) return "A-";
    else if (mark >= 75) return "B+";
    else if (mark >= 70) return "B";
    else if (mark >= 65) return "B-";
    else if (mark >= 60) return "C+";
    else if (mark >= 55) return "C";
    else if (mark >= 50) return "D";
    else if (mark >= 40) return "E";
    else return "F";
}

double gradeToPoint(string grade) {
    if (grade == "A+") return 4.0;
    else if (grade == "A") return 3.9;
    else if (grade == "A-") return 3.7;
    else if (grade == "B+") return 3.3;
    else if (grade == "B") return 3.0;
    else if (grade == "B-") return 2.7;
    else if (grade == "C+") return 2.3;
    else if (grade == "C") return 2.0;
    else if (grade == "D") return 1.3;
    else if (grade == "E") return 1.0;
    else return 0.0;
}


double calculateCPA(Subject subjects[], int numSubjects) {
    double totalPoints = 0, totalCredits = 0;
    for (int i = 0; i < numSubjects; i++) {
        totalPoints += gradeToPoint(subjects[i].grade) * subjects[i].credit;
        totalCredits += subjects[i].credit;
    }
    return (totalCredits > 0) ? totalPoints / totalCredits : 0;
}


void inputStudent(Student &s) {
    cout << "\nEnter student name: ";
    cin.ignore();
    getline(cin, s.name);
    cout << "Enter age: ";
    cin >> s.age;
    cout << "Enter number of subjects (max 5): ";
    cin >> s.numSubjects;

    if (s.numSubjects > 5) s.numSubjects = 5;

    for (int i = 0; i < s.numSubjects; i++) {
        cout << "\nSubject " << i + 1 << " name: ";
        cin.ignore();
        getline(cin, s.subjects[i].subjectName);

        cout << "Enter subject credit: ";
        cin >> s.subjects[i].credit;


        do {
            cout << "Enter mark (0 - 100): ";
            cin >> s.subjects[i].mark;
            if (s.subjects[i].mark < 0 || s.subjects[i].mark > 100)
                cout << "Invalid mark! Please enter between 0 and 100.\n";
        } while (s.subjects[i].mark < 0 || s.subjects[i].mark > 100);

        s.subjects[i].grade = calculateGrade(s.subjects[i].mark);
    }

    s.cpa = calculateCPA(s.subjects, s.numSubjects);
}


void displayStudent(const Student &s) {
    cout << fixed << setprecision(2);
    cout << "\n------------------------------------\n";
    cout << "Name: " << s.name << "\nAge: " << s.age << "\nCPA: " << s.cpa << endl;
    cout << "Subjects:\n";
    cout << left << setw(20) << "Subject" << setw(10) << "Credit"
         << setw(10) << "Mark" << setw(10) << "Grade" << endl;
    for (int i = 0; i < s.numSubjects; i++) {
        cout << left << setw(20) << s.subjects[i].subjectName
             << setw(10) << s.subjects[i].credit
             << setw(10) << s.subjects[i].mark
             << setw(10) << s.subjects[i].grade << endl;
    }
}

int main() {
    Student students[10];
    int numStudents;

    cout << "Enter number of students (max 10): ";
    cin >> numStudents;
    if (numStudents > 10) numStudents = 10;

    for (int i = 0; i < numStudents; i++) {
        cout << "\n--- Enter details for student " << i + 1 << " ---\n";
        inputStudent(students[i]);
    }

    cout << "\n\n========= Student Details =========\n";
    for (int i = 0; i < numStudents; i++) {
        displayStudent(students[i]);
    }

    return 0;
}
# Coding-to-Check-Student-s-Grades
