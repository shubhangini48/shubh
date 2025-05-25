import java.sql.*;
import java.util.ArrayList;
import java.util.List;


public interface DOA_lms {
    public class CourseDAO {
        private final String url = "jdbc:mysql://localhost:3306/your_database";
        private final String user = "root";
        private final String password = "W7301@jqir#";


        private Connection getConnection() throws SQLException {
            return DriverManager.getConnection(url, user, password);
        }

        // Create a new course
        public boolean addCourse(Course course) {
            String sql = "INSERT INTO Course (title, description, instructorId) VALUES (?, ?, ?)";

            try (Connection conn = getConnection();
                 PreparedStatement pstmt = conn.prepareStatement(sql)) {
                pstmt.setString(1, course.getTitle());
                pstmt.setString(2, course.getDescription());
                pstmt.setInt(3, course.getInstructorId());

                int rowsAffected = pstmt.executeUpdate();
                return rowsAffected > 0;
            } catch (SQLException e) {
                e.printStackTrace();
                return false;
            }
        }

        // Retrieve a course by ID
        public Course getCourse(int id) {
            String sql = "SELECT * FROM Course WHERE id = ?";

            try (Connection conn = getConnection();
                 PreparedStatement pstmt = conn.prepareStatement(sql)) {
                pstmt.setInt(1, id);
                ResultSet rs = pstmt.executeQuery();

                if (rs.next()) {
                    return new Course(
                            rs.getInt("id"),
                            rs.getString("title"),
                            rs.getString("description"),
                            rs.getInt("instructorId")
                    );
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
            return null;
        }

        // Update a course
        public boolean updateCourse(Course course) {
            String sql = "UPDATE Course SET title = ?, description = ?, instructorId = ? WHERE id = ?";

            try (Connection conn = getConnection();
                 PreparedStatement pstmt = conn.prepareStatement(sql)) {
                pstmt.setString(1, course.getTitle());
                pstmt.setString(2, course.getDescription());
                pstmt.setInt(3, course.getInstructorId());
                pstmt.setInt(4, course.getId());

                int rowsAffected = pstmt.executeUpdate();
                return rowsAffected > 0;
            } catch (SQLException e) {
                e.printStackTrace();
                return false;
            }
        }

        // Delete a course by ID
        public boolean deleteCourse(int id) {
            String sql = "DELETE FROM Course WHERE id = ?";

            try (Connection conn = getConnection();
                 PreparedStatement pstmt = conn.prepareStatement(sql)) {
                pstmt.setInt(1, id);
                int rowsAffected = pstmt.executeUpdate();
                return rowsAffected > 0;
            } catch (SQLException e) {
                e.printStackTrace();
                return false;
            }
        }

        // List all courses
        public List<Course> getAllCourses() {
            List<Course> courses = new ArrayList<>();
            String sql = "SELECT * FROM Course";

            try (Connection conn = getConnection();
                 Statement stmt = conn.createStatement();
                 ResultSet rs = stmt.executeQuery(sql)) {

                while (rs.next()) {
                    Course course = new Course(
                            rs.getInt("id"),
                            rs.getString("title"),
                            rs.getString("description"),
                            rs.getInt("instructorId")
                    );
                    courses.add(course);
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
            return courses;
        }
    }
    public class Course {
        private int id;
        private String title;
        private String description;
        private int instructorId;

        public Course(int id, String title, String description, int instructorId) {
            this.id = id;
            this.title = title;
            this.description = description;
            this.instructorId = instructorId;
        }

        // Getters and setters for each property
        public int getId() { return id; }
        public void setId(int id) { this.id = id; }
        public String getTitle() { return title; }
        public void setTitle(String title) { this.title = title; }
        public String getDescription() { return description; }
        public void setDescription(String description) { this.description = description; }
        public int getInstructorId() { return instructorId; }
        public void setInstructorId(int instructorId) { this.instructorId = instructorId; }
    }
    public class LMSApplication {
        public static void main(String[] args) {
            CourseDAO courseDAO = new CourseDAO();

            // Add a new course
            Course newCourse = new Course(0, "Java Programming", "Learn Java from scratch", 1);
            courseDAO.addCourse(newCourse);

            // Retrieve a course
            Course course = courseDAO.getCourse(1);
            System.out.println("Course Title: " + course.getTitle());

            // Update a course
            course.setTitle("Advanced Java Programming");
            courseDAO.updateCourse(course);

            // Delete a course
            courseDAO.deleteCourse(2);
        }
    }



}
