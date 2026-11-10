# Academic Information and Management System

## Project overview
This C++17 console program manages fictional students, instructors, courses, enrollments, grades, and academic reports. Users can add, update, view, and delete eligible records; enroll students; drop pending enrollments; enter grades; search students, instructors and courses by their identifiers, and sort all three record types; and generate transcripts and instructor teaching-load reports.

## Course concepts demonstrated
- **Abstract class and encapsulation:** `Person` declares a pure virtual `displayInfo()` and exposes controlled access to protected fields.
- **Inheritance and polymorphism:** `Student` and `Instructor` inherit `Person`; virtual `displayInfo()` is invoked through `Person` pointers.
- **Class template and custom data structure:** `HashTable<T>` implements a hash table with its own singly linked collision chains.
- **Operator overloading:** `Student` defines `==`, `<`, and `<<`.
- **Custom sorting:** `AcademicSystem::mergeSort()` sorts students by name or GPA; `mergeSortRecords()` is a reusable, stable recursive merge sort for instructors (name/ID) and courses (title/code/credits). No `std::sort` is used.
- **Recursion:** `countCompleted()` recursively counts completed enrollment records (simple traversal; not claimed as substantive recursion).

## Build and run
In a terminal opened in this folder:

```sh
g++ -std=c++17 -Wall -Wextra -Wpedantic main.cpp Person.cpp Student.cpp Instructor.cpp Course.cpp Enrollment.cpp HashTable.cpp AcademicSystem.cpp -o AcademicSystem.exe
```

Windows PowerShell: `./AcademicSystem.exe` (or `.\AcademicSystem.exe`).
Linux/macOS: compile with `-o academic_system` and run `./academic_system`.

Keep `academic_data.txt` beside the executable and run from this directory. The data is plain text and contains fictional records only.

## Current limitations and what I still need to improve
- Each course code represents one term's offering, so repeat enrollments across terms need a separate course-offering identifier.
- GPA supports letter grades A–F and does not implement plus/minus grades or withdrawals.
- Date/contact fields have limited format validation.
- Recursive counting is a simple traversal and could be redesigned for a more substantial use of recursion.
- This is a local educational application, not a secure student-record system.

## Feedback requested from classmates
1. Should I prioritize supporting course retakes and multiple term offerings, or improve validation and reporting first?
2. Is the class structure clear, or would you separate enrollment management from `AcademicSystem`?
3. Are there additional error cases or academic reports you would test or add?

## Repository contents
- `.cpp` and `.h`: project source code with header blocks and inline course-concept comments.
- `academic_data.txt`: fictional input records.
- `UML_Class_Diagram.png`: class relationships and key members.
- `UML_Activity_Diagram.png`: menu workflow and main actions.

**Module 1 proposal:** Add your original proposal to this repository (not included here because it was not supplied).
**Program screenshot:** Run the application locally and upload a screenshot of its actual output for the M4 draft deliverable.

## Search and sort (updated)
Main menu option **4 Search and sort** offers:
- 1: Find student by ID
- 2: Find course by code
- 3: Merge Sort students by name (A-Z) or GPA (high to low)
- 4: Find instructor by ID
- 5: Merge Sort instructors by name (A-Z) or ID
- 6: Merge Sort courses by title, code, or credits (high to low)

Main menu option **5 Reports** also provides sorted student, instructor, and course reports.
Merge Sort runs in O(n log n) time and O(n) auxiliary space. The hash table remains the student ID index; sorting uses temporary vectors and does not change saved record order.

**Diagram note:** The included UML images are the diagrams supplied with the project; the additional instructor/course sorting helpers and report options are not yet drawn individually in the class diagram.

## Compatibility
This version avoids `<filesystem>` so it can compile with older MinGW GCC 6.3 using the existing C++17 build command. Data saves still use a temporary file and a `.bak` backup.

## Menu organization (updated)

The main menu groups tasks by what users want to accomplish:

- **1 Manage records:** add, update, delete, or view student, instructor, and course records.
- **2 Enrollment and grades:** enroll students, drop pending enrollments, and enter/update grades.
- **3 Find and browse records:** look up a student/instructor/course or display sorted lists. Student, instructor, and course listings use custom Merge Sort.
- **4 Academic reports:** student transcript/GPA and instructor teaching load.
- **0 Save and exit.**

Changes are saved automatically after successful data modifications; the program also saves when exiting. The original UML activity image in this archive depicts the earlier menu layout and should be updated if submitted as a strict reflection of the current menu.
