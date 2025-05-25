//public class JDBC_lms
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.logging.Level;
import java.util.logging.Logger;


public class JDBC_lms {
    private static final Logger LOGGER = Logger.getLogger(JDBC_lms.class.getName());
    private static final String URL = "jdbc:mysql://localhost:3306/lmsdb?useSSL=false";
    private static final String USER = "root";
    private static final String PASSWORD = "W7301@jqir#";

    private Connection connection;

    public JDBC_lms() {
        try {
            connection = DriverManager.getConnection(URL, USER, PASSWORD);
            System.out.println("Database connected successfully.");
        } catch (SQLException e) {
            LOGGER.log(Level.SEVERE, "Database connection failed.", e);
            System.exit(1);
        }
    }

    public void createTables() {
        // SQL statements to create tables
        String createCoursesTable = "CREATE TABLE IF NOT EXISTS courses (" +
                "course_id INT PRIMARY KEY AUTO_INCREMENT," +
                "course_name VARCHAR(100) NOT NULL," +
                "description TEXT," +
                "instructor_id INT" +
                ");";

        String createInstructorsTable = "CREATE TABLE IF NOT EXISTS instructors (" +
                "instructor_id INT PRIMARY KEY AUTO_INCREMENT," +
                "name VARCHAR(100) NOT NULL," +
                "email VARCHAR(100) UNIQUE NOT NULL" +
                ");";

        String createStudentsTable = "CREATE TABLE IF NOT EXISTS students (" +
                "student_id INT PRIMARY KEY AUTO_INCREMENT," +
                "name VARCHAR(100) NOT NULL," +
                "email VARCHAR(100) UNIQUE NOT NULL" +
                ");";

        String createEnrollmentsTable = "CREATE TABLE IF NOT EXISTS enrollments (" +
                "enrollment_id INT PRIMARY KEY AUTO_INCREMENT," +
                "student_id INT," +
                "course_id INT," +
                "enrollment_date DATE," +
                "FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE," +
                "FOREIGN KEY (course_id) REFERENCES courses(course_id) ON DELETE CASCADE" +
                ");";

        try {
            // Creating tables
            try (PreparedStatement stmt1 = connection.prepareStatement(createCoursesTable)) {
                stmt1.executeUpdate();
                System.out.println("Courses table created or already exists.");
            }
            try (PreparedStatement stmt2 = connection.prepareStatement(createInstructorsTable)) {
                stmt2.executeUpdate();
                System.out.println("Instructors table created or already exists.");
            }
            try (PreparedStatement stmt3 = connection.prepareStatement(createStudentsTable)) {
                stmt3.executeUpdate();
                System.out.println("Students table created or already exists.");
            }
            try (PreparedStatement stmt4 = connection.prepareStatement(createEnrollmentsTable)) {
                stmt4.executeUpdate();
                System.out.println("Enrollments table created or already exists.");
            }
        } catch (SQLException e) {
            System.out.println("Table creation failed.");
            e.printStackTrace();
        }
    }

    public void addInstructor(String name, String email) {
        String insertInstructor = "INSERT INTO instructors (name, email) VALUES (?, ?);";
        try (PreparedStatement stmt = connection.prepareStatement(insertInstructor)) {
            stmt.setString(1, name);
            stmt.setString(2, email);
            stmt.executeUpdate();
            System.out.println("Instructor added successfully.");
        } catch (SQLException e) {
            System.out.println("Error adding instructor.");
            e.printStackTrace();
        }
    }

    public void addCourse(String courseName, String description, int instructorId) {
        String insertCourse = "INSERT INTO courses (course_name, description, instructor_id) VALUES (?, ?, ?);";
        try (PreparedStatement stmt = connection.prepareStatement(insertCourse)) {
            stmt.setString(1, courseName);
            stmt.setString(2, description);
            stmt.setInt(3, instructorId);
            stmt.executeUpdate();
            System.out.println("Course added successfully.");
        } catch (SQLException e) {
            System.out.println("Error adding course.");
            e.printStackTrace();
        }
    }

    public void enrollStudent(int studentId, int courseId) {
        String enrollStudent = "INSERT INTO enrollments (student_id, course_id, enrollment_date) VALUES (?, ?, CURDATE());";
        try (PreparedStatement stmt = connection.prepareStatement(enrollStudent)) {
            stmt.setInt(1, studentId);
            stmt.setInt(2, courseId);
            stmt.executeUpdate();
            System.out.println("Student enrolled successfully.");
        } catch (SQLException e) {
            System.out.println("Error enrolling student.");
            e.printStackTrace();
        }
    }

    public void displayCourses() {
        String selectCourses = "SELECT * FROM courses;";
        try (PreparedStatement stmt = connection.prepareStatement(selectCourses);
             ResultSet rs = stmt.executeQuery()) {
            System.out.println("Courses:");
            while (rs.next()) {
                System.out.println("ID: " + rs.getInt("course_id") + ", Name: " + rs.getString("course_name"));
            }
        } catch (SQLException e) {
            System.out.println("Error displaying courses.");
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        JDBC_lms lms = new JDBC_lms();
        lms.createTables();

        // Example usage
        lms.addInstructor("Dr. Smith", "smith@example.com");
        lms.addCourse("Introduction to Java", "Java programming basics.", 1);
        lms.enrollStudent(1, 1);
        lms.displayCourses();

    }
}
