import csv
import os

BUS_FILE = "buses.csv"

def initialize():
    if not os.path.exists(BUS_FILE):
        with open(BUS_FILE, "w", newline="") as file:
            writer = csv.writer(file)
            writer.writerow([
                "Bus ID",
                "Bus Name",
                "Source",
                "Destination",
                "Total Seats",
                "Available Seats",
                "Fare"
            ])

def add_bus():
    bus_id = input("Enter Bus ID: ")
    bus_name = input("Enter Bus Name: ")
    source = input("Enter Source: ")
    destination = input("Enter Destination: ")
    total_seats = int(input("Enter Total Seats: "))
    fare = float(input("Enter Fare: ₹"))

    with open(BUS_FILE, "a", newline="") as file:
        writer = csv.writer(file)
        writer.writerow([
            bus_id,
            bus_name,
            source,
            destination,
            total_seats,
            total_seats,
            fare
        ])

    print("\nBus added successfully!")

def view_buses():
    print("\n========== AVAILABLE BUSES ==========")

    with open(BUS_FILE, "r") as file:
        reader = csv.reader(file)

        for row in reader:
            print(row)

def search_bus():
    source = input("Enter Source: ").lower()
    destination = input("Enter Destination: ").lower()

    found = False

    with open(BUS_FILE, "r") as file:
        reader = csv.DictReader(file)

        for row in reader:
            if (row["Source"].lower() == source and
                    row["Destination"].lower() == destination):

                print("\nBus Found")
                print("-----------------------------")
                print("Bus ID :", row["Bus ID"])
                print("Bus :", row["Bus Name"])
                print("Seats :", row["Available Seats"])
                print("Fare : ₹", row["Fare"])

                found = True

    if not found:
        print("\nNo buses found.")

def menu():
    initialize()

    while True:

        print("\n==============================")
        print(" SMART BUS RESERVATION SYSTEM")
        print("==============================")

        print("1. Add Bus")
        print("2. View Buses")
        print("3. Search Bus")
        print("4. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            add_bus()
