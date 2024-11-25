# Health-care-consultation-management-project

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class User {
    protected String name;
    protected String email;
    
    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}

class Patient extends User {
    public Patient(String name, String email) {
        super(name, email);
    }
}

class Consultant extends User {
    private String specialization;

    public Consultant(String name, String email, String specialization) {
        super(name, email);
        this.specialization = specialization;
    }

    public String getSpecialization() {
        return specialization;
    }
}

class Consultation {
    private Patient patient;
    private Consultant consultant;
    private String date;
    private String time;
    
    public Consultation(Patient patient, Consultant consultant, String date, String time) {
        this.patient = patient;
        this.consultant = consultant;
        this.date = date;
        this.time = time;
    }
    
    public void displayConsultationDetails() {
        System.out.println("Consultation Details:");
        System.out.println("Patient: " + patient.getName() + " (" + patient.getEmail() + ")");
        System.out.println("Consultant: " + consultant.getName() + " (" + consultant.getSpecialization() + ")");
        System.out.println("Date: " + date);
        System.out.println("Time: " + time);
    }
}

class ConsultationService {
    private List<Consultation> consultations;
    
    public ConsultationService() {
        consultations = new ArrayList<>();
    }

    public void scheduleConsultation(Patient patient, Consultant consultant, String date, String time) {
        Consultation consultation = new Consultation(patient, consultant, date, time);
        consultations.add(consultation);
        System.out.println("Consultation scheduled successfully!");
    }

    public void viewConsultations() {
        if (consultations.isEmpty()) {
            System.out.println("No consultations scheduled.");
        } else {
            for (Consultation consultation : consultations) {
                consultation.displayConsultationDetails();
            }
        }
    }
}

public class HealthCareConsultantApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Create a few sample users
        Patient patient1 = new Patient("John Doe", "john@example.com");
        Consultant consultant1 = new Consultant("Dr. Smith", "dr.smith@example.com", "Cardiologist");
        Consultant consultant2 = new Consultant("Dr. Jane", "dr.jane@example.com", "Pediatrician");

        // Create the ConsultationService
        ConsultationService consultationService = new ConsultationService();
        while (true) {
            System.out.println("\nHealthcare Consultant System");
            System.out.println("1. Schedule a Consultation");
            System.out.println("2. View Scheduled Consultations");
            System.out.println("3. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine();  // Consume newline
            
            switch (choice) {
                case 1:
                    System.out.println("Enter consultation date (e.g., 2024-11-25): ");
                    String date = scanner.nextLine();
                    System.out.println("Enter consultation time (e.g., 10:00 AM): ");
                    String time = scanner.nextLine();
                    // For simplicity, assume patient1 and consultant1 are selected.
                    consultationService.scheduleConsultation(patient1, consultant1, date, time);
                    break;
                
                case 2:
                    consultationService.viewConsultations();
                    break;
                
                case 3:
                    System.out.println("Exiting system.");
                    scanner.close();
                    return;
                
                default:
                    System.out.println("Invalid option, try again.");
            }
        }
    }
}
