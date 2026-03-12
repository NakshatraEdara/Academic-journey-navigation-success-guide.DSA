import java.util.*;

// CO2: Linked List to store the "History" of your searches
class SearchNode {
    String searchDetail;
    SearchNode next;

    SearchNode(String detail) {
        this.searchDetail = detail;
        this.next = null;
    }
}

public class CollegePredictor {
    // CO3: Queue for "Notification Alerts" about counseling dates
    private static Queue<String> alerts = new LinkedList<>();
    
    // CO3: Stack to track "Favorite Colleges" (Undo/Last added)
    private static Stack<String> favorites = new Stack<>();

    // CO4: HashMap for fast lookup of "College Codes" and Seats
    private static HashMap<String, Integer> collegeSeats = new HashMap<>();

    private static SearchNode head = null;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        initializeColleges();

        System.out.println("=== Academic Journey: College Eligibility Predictor ===");

        while (true) {
            System.out.println("\n1. Predict Eligible Colleges (Sorting & Logic - CO1)");
            System.out.println("2. View Recent Search History (Linked List - CO2)");
            System.out.println("3. View Counseling Alerts (Queue - CO3)");
            System.out.println("4. Add to Favorite List (Stack - CO3)");
            System.out.println("5. Check Available Seats (Hashing - CO4)");
            System.out.println("6. Exit");
            System.out.print("Enter Choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter your Inter Percentage: ");
                    double inter = sc.nextDouble();
                    System.out.print("Enter your EAMCET Rank: ");
                    int rank = sc.nextInt();
                    
                    predictColleges(rank, inter); // CO1: Analysis & Logic
                    addToHistory("Rank: " + rank + ", Inter: " + inter + "%"); // CO2: Insertion
                    break;
                case 2:
                    displayHistory(); // CO2: Traversal
                    break;
                case 3:
                    System.out.println("Upcoming Alerts: " + alerts); // CO3: Queue View
                    break;
                case 4:
                    System.out.print("Enter College Name to Favorite: ");
                    sc.nextLine();
                    favorites.push(sc.nextLine()); // CO3: Stack Push
                    System.out.println("Added! Your latest favorite is on top.");
                    break;
                case 5:
                    System.out.print("Enter College Code (e.g., JNTU): ");
                    String code = sc.next().toUpperCase();
                    // CO4: Hashing for fast retrieval
                    if(collegeSeats.containsKey(code)) {
                        System.out.println("Available Seats in " + code + ": " + collegeSeats.get(code));
                    } else {
                        System.out.println("Invalid College Code.");
                    }
                    break;
                case 6:
                    System.exit(0);
            }
        }
    }

    // CO1: Logic for Eligibility and Sorting Rank Thresholds
    public static void predictColleges(int rank, double inter) {
        System.out.println("\n--- Based on your Rank " + rank + " ---");
        
        // Example logic for Hyderabad Colleges
        if (inter < 45.0) {
            System.out.println("Note: Minimum eligibility for most colleges is 45% in Inter.");
        } else {
            if (rank <= 5000) System.out.println("Eligible for: JNTU Hyderabad, OU Engineering College");
            else if (rank <= 15000) System.out.println("Eligible for: CBIT, VNR VJIET");
            else if (rank <= 30000) System.out.println("Eligible for: Vasavi, MVSR");
            else System.out.println("Eligible for: Various Private Engineering Colleges");
        }
    }

    // CO2: Adding to Linked List (History)
    public static void addToHistory(String data) {
        SearchNode newNode = new SearchNode(data);
        if (head == null) head = newNode;
        else {
            newNode.next = head;
            head = newNode;
        }
    }

    // CO2: Traversal of Linked List
    public static void displayHistory() {
        SearchNode temp = head;
        System.out.println("Recent Searches:");
        while (temp != null) {
            System.out.println("-> " + temp.searchDetail);
            temp = temp.next;
        }
    }

    public static void initializeColleges() {
        // CO4: Initialize Hash Data
        collegeSeats.put("JNTU", 600);
        collegeSeats.put("CBIT", 1200);
        collegeSeats.put("VNRV", 900);
        
        // CO3: Initialize Queue Data
        alerts.add("Slot Booking starts 15th March");
        alerts.add("Certificate Verification at Help Centers 20th March");
    }
}
