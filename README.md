possible_year_numbers = ("7", "8", "9", "10", "11")
possible_class_letters = ("A", "B", "C", "D", "E", "F")

year_number = (input("Enter a year number between Year 7 and 11: "))

while year_number not in possible_year_numbers:
  year_number = (input("\nThe value you entered must be a whole number between Year 7 and 11: "))
year_number = int(year_number)

class_letter = (input("Enter a letter from the following choices: A, B, C, D, E, F: ")).upper()
while class_letter not in possible_class_letters:
  class_letter = (input("Enter a letter from the following choices: A, B, C, D, E, F: ")).upper()

year_number = str(year_number)
T_grp = year_number , class_letter
print("The tutor group is " , "".join(T_grp))

Cand_amt = input("Please enter the total number of candidates in your group: ")
print("")
print("")

while int(Cand_amt) < 1 or int(Cand_amt) > 4:
    print("")
    Cand_amt = input("you have entered incorrect info. please try again: ")

Cand_amt = int(Cand_amt)

Stud_amt = input("Please enter the total number of students in your group: ")
print("")
print("")

 if int(Stud_amt) < 28 or int(Stud_amt) > 35:
     print("")
     Stud_amt = int(input("You have entered incorrect info. please try again: "))
     print("")

Stud_amt = int(Stud_amt)

Cand_names = [""] * Cand_amt
Abstain = 0

for i in range(Cand_amt):
    Cand_names[i] = input("please enter the name of the candidate: ")
print("")
print("")

print("The candidates that you can vote for are:", end=" ")
print(", ".join(Cand_names))
print("")
write_yes = True

def Voting():
    global write_yes
    global Cand_names
    global Cand_amt
    global Abstain
    global All_votes
    
    All_votes = [0] * Cand_amt
    IDDone = [0] * Stud_amt
    if write_yes == True:
        for i in range(Cand_amt):
            print("Type", i + 1, "to vote for: ", Cand_names[i])

        print("If you wish to not vote, press 0")
        print("Voting will now commence...")
        print("")
    counter = 0
    while counter < len(IDDone):
        print("(", counter + 1, "/", Stud_amt, ")", end=" ")
        ID = input("Please enter your ID: ")
        while ID in IDDone:
            print("This ID has already been used to vote, you may not vote again.")
    
        IDDone[counter] = ID
        print("your vote: ", end=" ")
        Vote = input()
        int_vote = int(Vote)
        if int_vote < 0 or int_vote > Cand_amt:
            Vote = input("You have entered incorrect info. please try again: ")

        for j in range(Cand_amt):
            if int_vote == j + 1:
                All_votes[j] += 1
                print(All_votes)
        if int_vote == 0:
            Abstain += 1
        counter += 1
        print("")
        print("")

    get_Winner()

def get_Winner():
    global Cand_amt
    global Cand_names
    global T_grp
    global All_votes
    global Abstain

    print("THE RESULT FOR YOUR GROUP NOW WILL BE PRESENTED,", T_grp,"WILL NOW BE PRESENTED...")
    print("")
    print("")
    winner = ""
    most = All_votes[0]
    countwinners = 0

    for i in range(Cand_amt):
        if All_votes[i] > most:
            most = All_votes[i]

    for i in range(Cand_amt):
        print("The candidate:", Cand_names[i])
        print("Number of votes:", All_votes[i])
        print("percentage of votes:", round((All_votes[i] / Stud_amt) * 100, 1), "%")
        print("")
    print("The number of abstained votes is: ", Abstain)
    
    for i in range(Cand_amt):
        if All_votes[i] == most:
            winner = Cand_names[i]
            countwinners = countwinners + 1

    if countwinners == 1:
        print("Thank you the vote is complete. The winner is", winner, "!!!")
    else:
        print("There is a tie. We will repeat the votes with the tied candidates: ")
        print("")
        print("")
        Abstain = 0
        NamesNewCandidates = [""]

        for i in range(Cand_amt):
            if All_votes[i] == most:
                NamesNewCandidates.append(Cand_names[i])
        NamesNewCandidates.pop(0)
        Cand_names = NamesNewCandidates
        Cand_amt = len(Cand_names)
        Voting()
Voting()
