import mysql.connector
mydb=mysql.connector.connect(host="localhost",user="root",password="Pavi@2003",database="amazondb")
mycursor=mydb.cursor()
print('WELCOME TO AMAZON')
print('***************************************************************************************************************')
print('ARE YOU NEW USER/EXISTING USER?'+'\n'+"1.NEW USER"+'\n'+"2.EXISTING USER")
def validate_login(username,mailid):
    mycursor.execute('select * from user_details where name like %s',(name,))
    data=mycursor.fetchall()
    username=data[0][1]
    mailid=data[0][2]
    if(username==name and mailid==mail_id):
        return 1
    else:
        print('INVALID LOGIN')   
def show_menu():   
    print("1.FASHION"+"\n"+"2.GROCERIES"+"\n"+"3.COSMETICS")  
    option=int(input("ENTER YOUR OPTION: "))
    total_cost=0
    if(option==1):
        mycursor.execute("select * from fashion")
        opt=mycursor.fetchall()
        print(opt)
        product_choice=int(input("ENTER YOUR CHOICE: "))
        if product_choice==1:
            count=int(input("NO. OF COUNT : "))
            total_cost+=(count * opt[product_choice-2][2])
            mycursor.execute("insert into order_details values(null,%s,%s,%s)",(opt[product_choice-1][1],count,total_cost,))
            mydb.commit()
        elif product_choice==2:
            count=int(input("NO OF COUNT : "))
            total_cost+=(count * opt[product_choice-2][2])
            mycursor.execute("insert into order_details values(null,%s,%s,%s)",(opt[product_choice-1][1],count,total_cost,))
            mydb.commit()
        elif product_choice==3:
            count=int(input('NO OF COUNT : '))
            total_cost+=(count * opt[product_choice-2][2])
            mycursor.execute("insert into order_details values(null,%s,%s,%s)",(opt[product_choice-1][1],count,total_cost,))
            mydb.commit()
        else:
            print("INVALID OPTION")
    else:
        print("INVALID OPTION")
user_choice=int(input())
if user_choice==1:
    name=input('ENTER YOUR NAME: ')
    mail_id=input('ENTER YOUR MAILID: ')
    phone_no=input('ENTER YOUR PHONENO: ')
    mycursor.execute("insert into user_details values(null,%s,%s,%s)",(name,mail_id,phone_no,))
    mydb.commit()
    print("REGISTERED SUCCESSFULLY")
if user_choice==2:
    name=input('ENTER YOUR NAME: ')
    mail_id=input('ENTER YOUR MAILID: ')
    if validate_login(name,mail_id):
        print("1.MENU")
        print("2.ORDER DETAILS")
        print("3.ACCOUNT")
        choice=int(input("ENTER YOUR CHOICE: "))
        if choice==1:
            cost=show_menu()
            print("ORDER IS SUCCESSFUL"+"/n"+"TOTAL COST = ",cost)



    

    
    
