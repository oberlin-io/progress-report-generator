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
