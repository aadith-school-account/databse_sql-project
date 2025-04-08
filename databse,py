import database, time, os



MENU_PROMPT = """-- Coffee Bean App --

Please choose one of these options:

1) Add a new bean.
2) See all beans.
3) Find a bean by name.
4) See which preparation method is best for a bean.
5) Sort by rating
6) Delete some beans by id/name
8) Exit.

Your selection:"""
###########-FUNCTIONS FOR BEANS-############
def clear_screen():
    os.system("clear")

def pause():
    input("Press enter to continue: ")

def prompt_add_beans(connection):
    name = input("Enter bean name: ")
    method = input("Enter how you've prepared it: ")
    rating = int(input("Enter your rating score (0-100): "))

    database.add_bean(connection, name, method, rating)

def see_all_beans(connection):
    # receives the connection for all beans
    beans = database.get_all_beans(connection)

    # for loop to print every bean
    for bean in beans:
        print(f"{bean[1]} ({bean[2]}) - {bean[3]}/100")

def find_bean(connection):
    # find beans based on input
    name = input("Enter bean name to find: ")
    beans = database.get_beans_by_name(connection, name)
    # print beans
    for bean in beans:
        print(f"{bean[1]} ({bean[2]}) - {bean[3]}/100")

def find_method(connection):
    name = input("Enter bean name to find: ")
    best_method = database.get_best_preparation_for_bean(connection, name)

    print(f"The best preparation method for {name} is {best_method[2]} ")

def wipe_beans():
    f = open('data.db', 'r+')
    f.truncate(0)  # need '0' when using r+

def delete_bean_id_name(connection):
    choice = input("""
    Would you like to...
    1) Delete bean by name
    2) Delete bean by ID 
    (Please input 1 or 2): """)

    if choice == "1":
        name = input("What is your beans name?: ")
        database.delete_bean_by_name(connection, name)
    elif choice == "2":
        id = input("What is your beans ID number?: ")
        database.delete_bean_by_ID(connection, id)

def sort_by_rating(connection):
    start_range = int(input("Please select the LOWEST rating(ONLY INTEGER VALUES): "))
    end_range = int(input("Please select the HIGHEST rating(ONLY INTEGER VALUES): "))

    beans = database.find_bean_by_range(connection, start_range, end_range)

    for bean in beans:
        print(f"{bean[1]} ({bean[2]}) - {bean[3]}/100")


#########-MAIN MENU-##########
def menu():
    connection = database.connect()
    database.create_tables(connection)
# := allows you to assign a value to a variable within an expression
    while (user_input := input(MENU_PROMPT)) != "8":
        if user_input == "1":
            prompt_add_beans(connection)
            pause()
        elif user_input == "2":
            see_all_beans(connection)
            pause()
        elif user_input == "3":
            find_bean(connection)
            pause()
        elif user_input == "4":
            find_method(connection)
            pause()
        elif user_input == "5":
            sort_by_rating(connection)
            pause()
        elif user_input == "6":
            delete_bean_id_name(connection)
            print("Your bean has been deleted :)")
            pause()
        elif user_input == "8":
            print("Bye!")
            wipe_beans()
        else:
            print("Invalid input")

menu()
