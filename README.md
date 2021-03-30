# BankChallenge
package com.company;

import java.util.ArrayList;

public class Customer {

    private String name;
    private ArrayList<Double> myTransactions;


    public Customer(String name) {
        this.name = name;
        this.myTransactions = new ArrayList<>();
    }

    public void addTransaction(double amt) {
        this.myTransactions.add(amt);
    }

    public String getName() {
        return name;
    }

    public ArrayList<Double> getTransactions() {
        return myTransactions;
    }

    public static Customer createCustomer(String name) {
        return new Customer(name);
    }


}
package com.company;

import java.beans.Customizer;
import java.util.ArrayList;


public class Branch {
    private ArrayList<Customer> myCustomer;
    private ArrayList<Double> myTransactions;
    private String branch;
    private String name;


    public Branch(String name) {

        this.myCustomer = new ArrayList<Customer>();
        this.myTransactions = new ArrayList<Double>();
        this.branch = branch;
        this.name = name;

    }

    public String getName() {
        return name;
    }

    public static Branch createBranch(String name) {
        return new Branch(name);
    }

    public String getBranch() {
        return branch;
    }

    public ArrayList<Customer> getCustomers() {
        return myCustomer;
    }

    public boolean addNewCustomer(Customer customer) {
        if (findCustomer(customer.getName()) >= 0) {
            System.out.println("Customer is not on file");
            return false;
        }

        myCustomer.add(customer);
        return true;
    }

    private int findCustomer(Customer customer) {

        return this.myCustomer.indexOf(customer);
    }

    private int findCustomer(String customerName) {
        for (int i = 0; i < this.myCustomer.size(); i++) {
            Customer customer = this.myCustomer.get(i);
            if (customer.getName().equals(customerName)) {
                return i;
            }
        }
        return -1;
    }

    public boolean addNewTransaction(String custName, double amt) {
        Customer existCust = findCust(custName);
        if (existCust != null) {
            existCust.addTransaction(amt);
            return true;
        }

        return false;
    }

    private Customer findCust(String custName) {
        for (int i = 0; i < this.myCustomer.size(); i++) {
            Customer checkedCust = this.myCustomer.get(i);
            return checkedCust;
        }
        return null;
    }


}

