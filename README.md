

<!---
Bismark-apt/Bismark-apt is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
public class Emolument {
    private double basic_salary;
    private double tax_relief;

    // Constructor
    public Emolument(double basic_salary, double tax_relief) {
        this.basic_salary = basic_salary;
        this.tax_relief = tax_relief;
    }

    // Getters
    public double getBasicsalary() {
        return basic_salary;
    }

    public double getTaxRelief() {
        return tax_relief;
    }

    // SSNIT Contribution (3.5% of Basic Salary)
    public double SSNIT() {
        return basic_salary * 0.035;
    }

    // Taxable Income
    public double taxableIncome() {
        return basic_salary - (tax_relief + SSNIT());
    }
}
public class Main {
    public static void main(String[] args) {
        Emolument employee = new Emolument(5000.00, 1000.00); 

        System.out.println("Basic Salary: " + employee.getBasicsalary());
        System.out.println("Tax Relief: " + employee.getTaxRelief());
        System.out.println("SSNIT Contribution: " + employee.SSNIT());
        System.out.println("Taxable Income: " + employee.taxableIncome());
    }
}
public class MyEmolument extends Emolument {
    // Encapsulated fields
    private double basic_salary;
    private double tax_relief;

    // Default constructor
    public MyEmolument() {
        super(0.0, 0.0); // Call the superclass constructor with default values
    }

    // Parameterized constructor
    public MyEmolument(double basic_salary, double tax_relief) {
        super(basic_salary, tax_relief); // Call the superclass constructor
    }

    // Method to calculate Income Tax
    public double incomeTax() {
        double taxableIncome = super.taxableIncome(); // Get taxable income from superclass

        double tax = 0.0;

        if (taxableIncome <= 500.00) {
            tax = taxableIncome * 0.05;
        } else if (taxableIncome <= 1000.00) {
            tax = (500.00 * 0.05) + ((taxableIncome - 500.00) * 0.125);
        } else {
            tax = (500.00 * 0.05) + (500.00 * 0.125) + ((taxableIncome - 1000.00) * 0.175);
        }

        return tax;
    }
}
import javax.swing.JOptionPane;

public class MyEmolument extends Emolument {
    // ... (Constructor and incomeTax() method as defined previously) ...

    public double totalDeduction() {
        return SSNIT() + incomeTax();
    }

    public double netSalary() {
        return getBasicsalary() - totalDeduction();
    }

    public static void main(String args) {
        String basicSalaryStr = JOptionPane.showInputDialog("Enter Basic Salary:");
        String taxReliefStr = JOptionPane.showInputDialog("Enter Tax Relief:");

        try {
            double basicSalary = Double.parseDouble(basicSalaryStr);
            double taxRelief = Double.parseDouble(taxReliefStr);

            MyEmolument Staff_Salary = new MyEmolument(basicSalary, taxRelief);

            JOptionPane.showMessageDialog(
                    null,
                    "Basic Salary: " + Staff_Salary.getBasicsalary() + "\n" +
                    "Tax Relief: " + Staff_Salary.getTaxRelief() + "\n" +
                    "SSNIT Contribution: " + Staff_Salary.SSNIT() + "\n" +
                    "Taxable Income: " + Staff_Salary.taxableIncome() + "\n" +
                    "Income Tax: " + Staff_Salary.incomeTax() + "\n" +
                    "Total Deduction: " + Staff_Salary.totalDeduction() + "\n" +
                    "Net Salary: " + Staff_Salary.netSalary()
            );
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(null, "Invalid input. Please enter valid numbers.", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }
}
