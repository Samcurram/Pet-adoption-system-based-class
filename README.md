# Pet-adoption-system-based-class:

import random

class Pet:
    def __init__(self, name, species, age):
        self.name = name
        self.species = species
        self.age = age

    def display_info(self):
        print(f"Name: {self.name}, Species: {self.species}, Age: {self.age}")

class Dog(Pet):
    def __init__(self, name, age, breed, color):
        super().__init__(name, "Dog", age)
        self.breed = breed
        self.color = color

    def display_info(self):
        super().display_info()
        print(f"Breed: {self.breed}, Color: {self.color}")

class Cat(Pet):
    def __init__(self, name, age, breed, color):
        super().__init__(name, "Cat", age)
        self.breed = breed
        self.color = color

    def display_info(self):
        super().display_info()
        print(f"Breed: {self.breed}, Color: {self.color}")

class PetAdoptionSystem:
    def __init__(self):
        self.pets = {}
        self.pet_preferences = {
            "Dog": ("Bones", "Walk"),
            "Cat": ("Fish", "Scratching Post")
        }

    def add_pet(self):
        name = input("Enter pet's name: ")
        species = input("Enter pet's species (Dog or Cat): ").capitalize()
        age = int(input("Enter pet's age: "))
        pet_id = random.randint(1000, 9999)  # Generate a unique 4-digit ID

        if species == "Dog":
            breed = input("Enter dog's breed: ")
            color = input("Enter dog's color: ")
            self.pets[pet_id] = Dog(name, age, breed, color)
        elif species == "Cat":
            breed = input("Enter cat's breed: ")
            color = input("Enter cat's color: ")
            self.pets[pet_id] = Cat(name, age, breed, color)
        else:
            print("Invalid species.")
            return

        print(f"Pet '{name}' added with ID: {pet_id}")

    def view_pets(self):
        if not self.pets:
            print("No pets available for adoption yet.")
            return
        print("\nAvailable Pets:")
        for pet_id, pet in self.pets.items():
            print(f"ID: {pet_id}", end=" | ")
            pet.display_info()
        print("-" * 20)

    def adopt_pet(self):
        pet_id_to_adopt = int(input("Enter the ID of the pet you want to adopt: "))
        if pet_id_to_adopt in self.pets:
            adopted_pet = self.pets.pop(pet_id_to_adopt)
            print(f"\nCongratulations! You've adopted:")
            adopted_pet.display_info()
            if adopted_pet.species in self.pet_preferences:
                preferences = self.pet_preferences[adopted_pet.species]
                print("Care Preferences:", ", ".join(preferences))
            print("-" * 20)
        else:
            print("Invalid pet ID.")

    def run_menu(self):
        while True:
            print("\nPet Adoption System Menu:")
            print("1. View Available Pets")
            print("2. Add a Pet")
            print("3. Adopt a Pet")
            print("4. Exit")

            choice = input("Enter your choice: ")

            if choice == '1':
                self.view_pets()
            elif choice == '2':
                self.add_pet()
            elif choice == '3':
                self.adopt_pet()
            elif choice == '4':
                print("Thank you for visiting the Pet Adoption System!")
                break
            else:
                print("Invalid choice. Please try again.")

# Let's create an instance of the system and run the menu
if __name__ == "__main__":
    adoption_system = PetAdoptionSystem()
    adoption_system.run_menu()
