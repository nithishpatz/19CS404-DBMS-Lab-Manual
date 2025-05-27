# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Student Name

## Scenario Chosen:
University 

## ER Diagram:

![438631459-469fcbf7-49c2-434c-9374-52161dc36bd5](https://github.com/user-attachments/assets/2523451c-a46b-4b4a-818a-a0ec2c1e56d4)

## Entities and Attributes:
-COURSE: COURSE_NAME, COURSE_ID, PREREQUISITE,NO_OF_CREDITS. <br/>
-STUDENT: REG_NO, STUDENT_NAME,EMAIL,PHONE_NO,D.O.B. <br/>
-INSTRUCTOR:NAME,STAFF_ID,CONTACT,EMAIL,PHONE_NO. <br/>


## Relationships and Constraints:
* TEACHES:
INSTRUCTOR teaches COURSE
(Implies a one-to-many relationship where one instructor can teach multiple courses, but each course is taught by one instructor. Participation likely total for COURSE and partial for INSTRUCTOR).ENROLLMENT:
* STUDENT enrolls in COURSE
(Cardinality and Participation are not explicitly shown, but it implies a many-to-many relationship where a student can enroll in multiple courses, and each course can have multiple students. Participation is likely total for ENROLLMENT and partial for both STUDENT and COURSE).
* PREREQUISITE:
COURSE has PREREQUISITE
(Reflexive relationship on COURSE, implying that a course can have one or more prerequisite courses, and can be a prerequisite for others. Likely an optional many-to-many relationship. Participation is likely partial on both sides).


## Extension (Prerequisite / Billing):

* Prerequisite: Prerequisites are modeled through a reflexive relationship on the COURSE entity. The attribute
PREREQUISIT (which should likely be PREREQ_ID to reference another course's ID) in the COURSE entity indicates which course(s)
are required before taking a particular course. This structure allows for defining chains or multiple prerequisites for a single course.

* Billing: Billing information is partially modeled through the FEE attribute in the STUDENT entity. This suggests that each student
has an associated fee. However, the diagram doesn't provide details on when or how these fees are applied (e.g., per program, per
semester, per course) or any information about payment status, due dates, or billing history. To model billing more comprehensively,
 you might need additional entities like BILL, PAYMENT, or a more detailed structure within the REGISTRATION or a new enrollment-specific entity to track financial aspects.


## Design Choices:
This ER diagram provides a good foundation for a student registration system, capturing key entities and their relationships.
However, depending on the specific requirements, further refinement might be needed, especially in areas like billing and a clearer
definition of the 'TYPE' attribute in the REGISTRATION entity.

## RESULT
Thus ENROLLMENT relationship indicates that a student can enroll in multiple courses and each course can have many students, allowing the system to track which students are taking which courses. The TEACHES relationship shows that one instructor can teach multiple courses, but each course is taught by only one instructor, assigning teaching responsibilities clearly.
