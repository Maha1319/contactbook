main.py:

from contact_book import ContactBook


def display_menu():
    print("\nContact Book Application")
    print("1. Add Contact")
    print("2. View Contacts")
    print("3. Search Contact")
    print("4. Update Contact")
    print("5. Delete Contact")
    print("6. Exit")


def main():
    contact_book = ContactBook()

    while True:
        display_menu()
        choice = input("Enter your choice: ")

        if choice == '1':
            name = input("Enter name: ")
            phone = input("Enter phone number: ")
            email = input("Enter email: ")
            address = input("Enter address: ")
            contact_book.add_contact(name, phone, email, address)
        elif choice == '2':
            contact_book.view_contacts()
        elif choice == '3':
            search_term = input("Enter name or phone number to search: ")
            contact_book.search_contact(search_term)
        elif choice == '4':
            name = input("Enter the name of the contact to update: ")
            new_name = input("Enter new name (leave blank to keep current): ")
            new_phone = input("Enter new phone number (leave blank to keep current): ")
            new_email = input("Enter new email (leave blank to keep current): ")
            new_address = input("Enter new address (leave blank to keep current): ")
            contact_book.update_contact(name, new_name, new_phone, new_email, new_address)
        elif choice == '5':
            name = input("Enter the name of the contact to delete: ")
            contact_book.delete_contact(name)
        elif choice == '6':
            print("Exiting the application.")
            break
        else:
            print("Invalid choice. Please try again.")


if _name_ == "_main_":
    main()

contact.py

class Contact:
    def _init_(self, name, phone, email, address):
        self.name = name
        self.phone = phone
        self.email = email
        self.address = address

    def _str_(self):
        return f"Name: {self.name}, Phone: {self.phone}, Email: {self.email}, Address: {self.address}"

    def update(self, name=None, phone=None, email=None, address=None):
        if name:
            self.name = name
        if phone:
            self.phone = phone
        if email:
            self.email = email
        if address:
            self.address = address

contact_book.py:

from contact import Contact

class ContactBook:
    def _init_(self):
        self.contacts = []

    def add_contact(self, name, phone, email, address):
        contact = Contact(name, phone, email, address)
        self.contacts.append(contact)
        print(f"Contact {name} added successfully.")

    def view_contacts(self):
        if not self.contacts:
            print("No contacts available.")
        else:
            for idx, contact in enumerate(self.contacts, start=1):
                print(f"{idx}. {contact.name} - {contact.phone}")

    def search_contact(self, search_term):
        results = [contact for contact in self.contacts if search_term in contact.name or search_term in contact.phone]
        if not results:
            print("No contacts found.")
        else:
            for contact in results:
                print(contact)

    def update_contact(self, name, new_name=None, new_phone=None, new_email=None, new_address=None):
        for contact in self.contacts:
            if contact.name == name:
                contact.update(new_name, new_phone, new_email, new_address)
                print(f"Contact {name} updated successfully.")
                return
        print(f"Contact {name} not found.")

    def delete_contact(self, name):
        for contact in self.contacts:
            if contact.name == name:
                self.contacts.remove(contact)
                print(f"Contact {name} deleted successfully.")
                return
        print(f"Contact {name} not found.")
