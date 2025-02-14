
CREATE TABLE IF NOT EXISTS public."ASSIGNMENT"
(
    assignment_id integer NOT NULL,
    assignment character varying(100) COLLATE pg_catalog."default" NOT NULL,
    student_id integer NOT NULL,
    department_id integer NOT NULL,
    submit_date date NOT NULL,
    teacher_id integer,
    CONSTRAINT "ASSIGNMENT_pkey" PRIMARY KEY (assignment_id)
);

CREATE TABLE IF NOT EXISTS public."DEPARTMENT"
(
    department_id integer NOT NULL,
    "department name" character varying(250) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT "DEPARTMENT_pkey" PRIMARY KEY (department_id)
);

CREATE TABLE IF NOT EXISTS public."ENROLLMENT"
(
    enrollment_id integer NOT NULL,
    student_id integer NOT NULL,
    enrollment_date date NOT NULL,
    CONSTRAINT "ENROLLMENT_pkey" PRIMARY KEY (enrollment_id)
);

CREATE TABLE IF NOT EXISTS public."FEES"
(
    fees_id integer NOT NULL,
    student_id integer NOT NULL,
    amount numeric NOT NULL,
    due_date date NOT NULL,
    paid_date date,
    CONSTRAINT "FEES_pkey" PRIMARY KEY (fees_id)
);

CREATE TABLE IF NOT EXISTS public."GRADE"
(
    grade_id integer NOT NULL,
    enrollment_id integer NOT NULL,
    garde "char" NOT NULL,
    CONSTRAINT "GRADE_pkey" PRIMARY KEY (grade_id)
);

CREATE TABLE IF NOT EXISTS public."STUDENTS"
(
    student_id integer NOT NULL,
    name character varying(250) COLLATE pg_catalog."default" NOT NULL,
    dob date NOT NULL,
    phone_no numeric NOT NULL,
    CONSTRAINT "STUDENTS_pkey" PRIMARY KEY (student_id)
);

CREATE TABLE IF NOT EXISTS public."TEACHERS"
(
    teacher_id integer NOT NULL,
    name character varying(250) COLLATE pg_catalog."default" NOT NULL,
    department character varying(250) COLLATE pg_catalog."default" NOT NULL,
    phone_no numeric NOT NULL,
    CONSTRAINT "TEACHERS_pkey" PRIMARY KEY (teacher_id)
);

ALTER TABLE IF EXISTS public."ASSIGNMENT"
    ADD CONSTRAINT "STUDENT_ID" FOREIGN KEY (student_id)
    REFERENCES public."STUDENTS" (student_id) MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;


ALTER TABLE IF EXISTS public."ASSIGNMENT"
    ADD CONSTRAINT "TEACHER_ID" FOREIGN KEY (teacher_id)
    REFERENCES public."TEACHERS" (teacher_id) MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;


ALTER TABLE IF EXISTS public."ASSIGNMENT"
    ADD CONSTRAINT "DEPARTMENT_ID" FOREIGN KEY (department_id)
    REFERENCES public."DEPARTMENT" (department_id) MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;


ALTER TABLE IF EXISTS public."ENROLLMENT"
    ADD CONSTRAINT "STUDENT_ID" FOREIGN KEY (student_id)
    REFERENCES public."STUDENTS" (student_id) MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;


ALTER TABLE IF EXISTS public."FEES"
    ADD CONSTRAINT "STUDENT_ID" FOREIGN KEY (student_id)
    REFERENCES public."STUDENTS" (student_id) MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;


ALTER TABLE IF EXISTS public."GRADE"
    ADD CONSTRAINT "ENROLLMENT_ID" FOREIGN KEY (enrollment_id)
    REFERENCES public."ENROLLMENT" (enrollment_id) MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;

END;
