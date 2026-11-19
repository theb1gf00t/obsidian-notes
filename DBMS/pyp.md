---
title: DBMS — Previous Year Question Paper
tags:
  - dbms
  - pyp
---

# DBMS — Previous Year Question Paper

*Source: [[prev_year.pdf]] — Max Marks: 100, Max Time: 180 Min.*

> [!question] Q1: Normalization — relational schema design (40M)
> Apply efficient algorithms (Normalization) to the following user requirements to generate a relational schema from a universal relation for the following requirements — Governor of a fictional state wanted a portal for a crime management system with the clearly illustrated. The relational schema should be in 3NF/BCNF. All the steps should be followed.
>
> Every police officer will be listed in the portal along with the details like empid, name, designation, DoJ, DoB, office address, latest photo etc. Every district will have a Deputy Commissioner of Police responsible for completing all the investigations within the district. All the Deputy Commissioners will report to the Commissioner of Police, who is responsible for completing all the investigations in the state.
>
> A user can register in the portal with details like name, mobile number, address, etc. After registration, a user can file a complaint, and the complaint will be assigned by the Deputy Commissioner to a Team of 2 to 5 Police officers, depending on the gravity of the complaint/crime. The senior officer will lead the Team. Every Team is identified with an ID, and it has a contact no, email, etc. The Team will resolve every complaint within 15 days. Every case/complaint will have a unique case file maintained by the Team with the details of the complainant, accused and progress. The details (name, age, gender, DoB, Biometrics, etc.) of every accused are stored, and an accused is uniquely identifiable. Every Police officer is assigned at most ten cases in a month.
>
> All the Police officers within a district report to the senior officer in the Deputy Commissioner of Police. The Deputy Commissioner will monitor every case filed by the user. The senior officer will finalize the investigation report after he/she is satisfied with it. During this stage, if it is felt that the investigation is lacking in a few aspects, then a larger team will be constituted by the Deputy Commissioner to reinvestigate the complaint. After a satisfactory report from the Team, the Deputy Commissioner will approve the report, and it will be available for the user. If the user is satisfied with the report, the Team will file the case in court, and the court will give the final judgment within 15 days.
>
> The court will hear the case on a daily basis. Each court is uniquely identified and has an address, phone number, etc. Both the parties will be represented by the lawyers. A lawyer has a name, DoB, address, etc., stored in the portal. A lawyer can be associated with many courts. If the court convicts the accused as reported by the Team, then the entire Team will be rewarded for conducting a foolproof investigation in accordance with the law.
>
> *NOTE: All the attributes are not mentioned in the description — you are expected to identify at least a few of them.*

> [!question] Q2: Lossless vs. dependency-preserving decomposition (10M)
> Prove or disprove the following statements:
> a) If a decomposition is lossless then it will always preserve the dependencies.
> b) If a decomposition is dependency preserving then it will always be lossless.

> [!question] Q3: Query optimization — relational algebra steps (12M)
> Apply query optimization on the following expression and illustrate **all the steps**:
>
> `<select p.empId, p.name, p.phone from professor p, teaching t, enrollment e where e.rollNo = "CS22B999" and e.year = 2024 and e.courseId = t.courseId and e.sem = "even" and e.empId = t.empId> (2024 and t.sem = "even")`
>
> *(Note: expression as printed in the paper — condition clauses split across the line break: `e.rollNo = "CS22B999"` and `e.year = 2024` and `e.courseId = t.courseId` and `e.sem = "even"` and `t.sem = "even"` and `t.year = 2024` and `p.empId = t.empId`.)*

> [!question] Q4: View and conflict serializability (12M)
> Explain View and Conflict Serializability with the help of four transactions (each with at least three valid instructions) on two data items (X and Y), and by using the same requirements, answer the following questions:
> a) Give a schedule that is conflict serializable (justify using precedence graph).
> b) Give a schedule that is not conflict serializable (justify using precedence graph).

> [!question] Q5: B+ tree insertion and deletion (14M)
> Assume that block pointer and record pointer are of the same size, order $m$ is 3 and $m_{leaf}$ is 2. Insert the following elements into a B+ tree (one illustration for each insertion): 70, 19, 22, 3, 19, 17, 2, 83, 11, 39, 94, 69 and 61.
>
> Followed by delete the elements till a **level drop** (one illustration for each deletion).

> [!question] Q6: Weak entity vs. composite multi-valued attribute (10M)
> Discuss with an illustration the design choice between a weak entity and a composite multi-valued attribute.
>
> *(Marginal note in paper: "Go with illustration. ERD should be given pictorially.")*

> [!question] Q7: Unsafe TRC expression (2M)
> Give an example of an unsafe TRC expression.
