# grocerylist
# Add, remove, ban, unban, and clear items from the list. This is my first project. I just started programming a couple weeks ago.
import time

banning = open("banned.txt", "r")
shop = open("list.txt", "r")
banned = ""
shopping = ""
for item in banning:
    banned += item
banned = banned.split(", ")
for item in shop:
    shopping += item
shopping = shopping.split(", ")
shop.close()
banning.close()
password = "password"


def leave():
    global banning
    global shop
    global banned
    global shopping
    print("Loading")
    time.sleep(.4)
    print("Loading.")
    time.sleep(.4)
    print("Loading..")
    time.sleep(.4)
    print("Loading...")
    time.sleep(.4)
    print("Loading")
    time.sleep(.4)
    print("Loading.")
    time.sleep(.4)
    print("Loading..")
    time.sleep(.4)
    print("Loading...")
    time.sleep(.4)
    banning = open('banned.txt', "w")
    shop = open('list.txt', "w")
    b = ""
    s = ""
    if banned[0] == "":
        banned.remove(banned[0])
    if shopping[0] == "":
        shopping.remove(shopping[0])
    if len(banned) > 1:
        for item in banned[:-1]:
            b += item + ", "
        b = b + str(banned[-1])
        banning.write(b)
    else:
        if not banned:
            banning.write("")
        else:
            b = str(banned[0])
            banning.write(b)
    if len(shopping) > 1:
        for item in shopping[:-1]:
            s += item + ", "
        s = s + str(shopping[-1])
        shop.write(s)
    else:
        if not shopping:
            shop.write("")
        else:
            s = str(shopping[0])
            shop.write(s)
    banning.close()
    shop.close()
    print("Saved Successfully")
    exit()


def main(password = "password"):
    global shopping
    global banned
    global shop
    global banning

    add = ""
    remove = ""
    inputt = "   "
    ban = ""
    unban = ""
    removal = []
    while inputt not in "a r A R V v b B ub UB uB Ub e E c C":
        inputt = input("Would you like to exit, add or remove an item, view the list, ban an item, unban an item or "
                       "clear the list? "
                       "\nE  (exit and save)\nA  (add) \nR  (remove) \nV  (view)\nB  (ban)\nUB (unban)\nC  (clear):")

    if inputt in "a A ":
        add = input("What would you like to add to the list? If multiple items, separate with commas."
                    " If this was a misinput enter GB:")
        if add in "gb Gb GB gB ":
            main()
        else:
            add = add.split(", ")
            for item in add:
                if item in shopping:
                    print(f"\n{item} is a duplicate I will remove it.\n")
                    add = [x for x in add if x not in shopping]
            for item in add:
                if item in banned:
                    print(f"{item} is banned you cannot add it to the list.")
                    add = [x for x in add if x not in banned]
            shopping = shopping + add
            print()
            print(shopping)
            main()

    elif inputt in "r R ":
        remove = input(f"What would you like to remove from the list?{shopping} "
                       "If multiple items then separate with commas. Also, ensure correct spelling."
                       " If this was a misinput enter GB:")
        if remove in "gb Gb GB gB ":
            main()
        else:
            remove = remove.split(", ")
            print(remove)
            shopping = [x for x in shopping if x not in remove]
            print()
            print(shopping)
            print()
            main()

    elif inputt in "v V ":
        j = ",".join(shopping)
        for item in shopping:
            print(item)
        main()

    elif inputt in "b B ":
        while inputt != password:
            inputt = input("Enter Password")
        ban = input("What item would you like to ban? If there is more than one item separate items with a comma."
                    " If this was a misinput enter GB:")
        if ban in "gb Gb GB gB ":
            main()
        else:
            banned = banned + ban.split(", ")
            print(f"Banned - {banned}\n")
            items = ""
            why = "n"
            for items in shopping:
                if items in banned:
                    why = input(f"Would you like to remove newly banned item {items} from the list? Y OR N:")
            if why in "y Y ":
                shopping = [x for x in shopping if x not in banned]
                main()
            else:
                main()

    elif inputt in "ub UB uB Ub ":
        while inputt != password:
            inputt = input("Enter Password:")
        unban = input("What item would you like to unban? If multiple items separate with commas."
                      " If this was a misinput enter GB:")
        if unban in "gb Gb GB gB ":
            main()
        else:
            if "," in unban:
                unban = unban.split(", ")
            else:
                unban = [unban]
            banned = [x for x in banned if x not in unban]
            main()

    elif inputt in "c C ":
        inputt = input("Are you sure you want to clear the list? Y OR N:")
        if inputt in "y Y ":
            shopping = ['']
            main()
        else:
            main()
    else:
        print(f"Groceries: {shopping}")
        print(f"Banned items: {banned}")
        leave()


def intro():
    print("Make sure to save your changes by exiting the program correctly.")
    burger = input("Press enter to start.")

intro()
main()
