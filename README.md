# Contact-Management-System
import json

CONTACTS_FILE = "contacts.json"

# Load contacts from file
def load_contacts():
    try:
        with open(CONTACTS_FILE, "r") as file:
            return json.load(file)
    except (FileNotFoundError, json.JSONDecodeError):
        return []

# Save contacts to file
def save_contacts(contacts):
    with open(CONTACTS_FILE, "w") as file:
        json.dump(contacts, file, indent=4)

# Add a new contact
def add_contact():
    name = input("Enter Name: ")
    phone = input("Enter Phone Number: ")
    email = input("Enter Email Address: ")
    contacts.append({"name": name, "phone": phone, "email": email})
    save_contacts(contacts)
    print("Contact added successfully!\n")

# View contacts
def view_contacts():
    if not contacts:
        print("No contacts found.\n")
    else:
        for index, contact in enumerate(contacts, start=1):
            print(f"{index}. Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")
        print()

# Edit a contact
def edit_contact():
    view_contacts()
    try:
        index = int(input("Enter contact number to edit: ")) - 1
        if 0 <= index < len(contacts):
            contacts[index]["name"] = input("Enter New Name: ")
            contacts[index]["phone"] = input("Enter New Phone Number: ")
            contacts[index]["email"] = input("Enter New Email Address: ")
            save_contacts(contacts)
            print("Contact updated successfully!\n")
        else:
            print("Invalid contact number!\n")
    except ValueError:
        print("Invalid input!\n")

# Delete a contact
def delete_contact():
    view_contacts()
    try:
        index = int(input("Enter contact number to delete: ")) - 1
        if 0 <= index < len(contacts):
            contacts.pop(index)
            save_contacts(contacts)
            print("Contact deleted successfully!\n")
        else:
            print("Invalid contact number!\n")
    except ValueError:
        print("Invalid input!\n")

# Main menu
def main():
    global contacts
    contacts = load_contacts()
    while True:
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Edit Contact")
        print("4. Delete Contact")
        print("5. Exit")
        choice = input("Enter your choice: ")
        if choice == "1":
            add_contact()
        elif choice == "2":
            view_contacts()
        elif choice == "3":
            edit_contact()
        elif choice == "4":
            delete_contact()
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice! Please try again.\n")

if __name__ == "__main__":
    main()

