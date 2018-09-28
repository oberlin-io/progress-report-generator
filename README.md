# progress-report-generator
Efficiently create student progress reports aligned with teaching materials with Google Sheets

The intended output for student progress reports is an overview of each student's proficiency on the four skills of language (speaking, listening, writing, and reading) and behavior. Being that the weekly process can be quite tedious, the progress reports became known as the "paste" reports, as in copy-and-paste.

The generator I've developed removes the tedious nature of the task, while increasing its alignment with the curriculum and standardizing benchmarks.

The project joins a student table, a skill bank table, and a proficiency table on student ID, skill ID, and proficiency ID.

The skill bank includes the learning goals per book and lesson and must start with a verb infinitive, for example a learning goal for pronoun referents may look like:

> read a short paragraph containing pronoun references and supply the referent for a specific subject. The instructor reviewed the logic behind referents.

The proficiency table includes a variety of subject-verb constructions per proficiency level, for example a -1 proficiency may read:

> The student struggles to

The student table includes a list of students, skills, and week dates. The user selects a learning goal and proficiency for each student and skill.

Finally, the report tab takes the date and student ID to generate comments for each skill, combing learning goals and proficiency levels, for example:

> Reading: The student struggles to read a short paragraph containing pronoun references and supply the referent for a specific subject. The instructor reviewed the logic behind referents.

The following is the main set of QUERY() functions that build the skill comment.

Here, A5 = The skill, eg Reading.

The first QUERY() function is on the PROF table and selects the proficiency text based on a proficiency ID, eg -1. That ID must be queried from the student table, here named CPR. From that table, the proficiency ID is drawn based on multiple conditions, eg the date, student ID, and skill.

Those results are concatenated with a third query and another embedded query on the student table in order to output the skill text from the skill bank.

```
=
A5 &
": " &
QUERY(
        PROF!$A$2:$B,
        "SELECT B WHERE A = '" & QUERY(
                CPR!$A$2:$G,
                "SELECT G WHERE A = '" & $B$1 & "' AND C = '" & $B$2 & "' AND B = '" & A5 & "'",
                0
        ) & "'",
        0
) &
" " &
QUERY(
        BANK!$A$2:$E,
        "SELECT E WHERE D = '" & QUERY(
                CPR!$A$2:$G,
                "SELECT F WHERE A = '" & $B$1 & "' AND C = '" & $B$2 & "' AND B = '" & A5 & "'",
                0
        ) & "'",
        0
)
'''
