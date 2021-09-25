# Library-Management-By-Abhishek-Sharma
import os
import string
import pandas as pd
import xlwt
student_index=[]
bookNo =[]

# Library Class
class library:
	#  Constructor Library Class
	def __init__(self, bookData,studentData):
		self.book_data = bookData
		self.student_data = studentData
		
		# Display Books Function
	def display(self):
		print("\n============= All Books Present In Library =============\n")
		print(f"{self.book_data} \n") 
	
	# Return Book Library Details
	def returnBook(self, Book):
		for index, item in (self.book_data).iterrows():
			if Book in item['Books Name']:
				temp = item['No Of Books']
				if str(temp) < str(item['Total Book']):
					(self.book_data).loc[index,'No Of Books'] = temp+1
					(self.book_data).to_excel("Books_data.xls",index = False)
					(self.student_data).loc[student_index[0], f"Book-{str(bookNo[0])}"] =""
					(self.student_data).to_excel("Student_data.xls",index = False)
					print("====== Successfully Return The Book ======")
					return 0
        
				else:
					print("---------------------------------------------------------------")
					print("_______This Book Not Library Book_______")
		
					
		# Issue Book Function Details Library					
	def requestBook(self):
		bookIndex = int(input("Enter The Book S No.  : ")) 
		for index, item in (self.book_data).iterrows():
			if str(bookIndex) == str(item['Sno']):
				temp = item['No Of Books']
				if temp >0:  
						(self.book_data).loc[index,'No Of Books'] = temp-1
						reqBookName = item['Books Name']
						print("---------------------------------------------------------------")
						print(f"Book Name : {reqBookName}")
						print("---------------------------------------------------------------")
						return reqBookName
				else:
					return ""
				
	
	
# Student Class
class Student: 
  # Constructor
  def __init__(self, data,bookData):
  	self.student_data = data
  	self.book_data = bookData
  	
  	# Return Book Function Student Details
  def returnBookStudent(self):
    rollNo =input("Enter The Student Roll No : ") 
    bookName = self.studentDetails (rollNo)
    return bookName
     
    # Book Issue Function Student Details          
  def issueBookStudent(self,reqBookName):
   if str(reqBookName).lower() != "none" :
   	rollNo = input("Enter The Student Roll No.  : ")
   	for index, item in (self.student_data).iterrows():
					if rollNo == str(item['Roll No']):
								print("---------------------------------------------------------------")
								print("\n__________Student Details__________")
								print(item) 
								block = int(input("Select The Book Block : "))
								block = f"Book-{str(block)}"
								if str(item[block]).lower() == "nan":
									  (self.student_data).loc[index, block] = reqBookName
									  (self.book_data).to_excel("Books_data.xls",index = False)
									  (self.student_data).to_excel("Student_data.xls",index = False)
									  print("---------------------------------------------------------------")
									  print("======== Successfully Issue Book ========") 
									  return 0
								else:
										print("---------------------------------------------------------------")
										print("This Block Location Book Already Issue")
										return 0
									
   	else:
   			print("---------------------------------------------------------------")
   			print("This Roll No Not Register In Library.")
									  	  
							
   else:
      print("---------------------------------------------------------------")
      print("This Location Not Register Any Book. Please Try Again With Right Index Book")
     		
     		

  # Find Student Details
  def studentDetails(self, rollNo):
    for index, item in (self.student_data).iterrows():
      if rollNo in str(item['Roll No']):
        print("\n######### Student Details #########")
        print(f"{item}\n")
        choiceBook = input("Enter The Return Book Number : ")
        bookName = item[f'Book-{str(choiceBook)}']
       
        if str(bookName).lower() != "nan":
        	print(bookName)
        	student_index.append(index) 
        	bookNo.append(choiceBook) 
        	return bookName
        else:
        	print("========== Any Book Not Issue ==========")
        	return 0
    else:
        	print("This Roll No Not Register In Library. ")
        	
        	
        	
# All Student Data Show Class & Function
class StudentInfo:
	def __init__(self, studentInfo):
		self.student_info = studentInfo
		
		# Display Function
	def display(self):
		print("\n____________________All Student Details____________________")
		for index, item in (self.student_info).iterrows():
			print("---------------------------------------------------------------")
			
			print(f"{item['Roll No']}   {item['Name']}   {item['Book-1']}   {item['Book-2']}    {item['Book-3']}  ")

		
						
#  Class New Data Add In Data Base( cls Files)	    
class NewDataAdd:
	def __init__(self,studentData,bookData):
		self.student_data = studentData
		self.book_data = bookData
		
		# Add New Book Library 
	def addBooks(self):
		count =0
		try:
			noOfBooks = int(input("Enter The Number Of Books : ")) 
			bookNames = input("Enter The Book Names : ")
			for index, item in (self.book_data).iterrows():
				count = index
			(self.book_data).loc[index+1, "No Of Books"] = noOfBooks
			(self.book_data).loc[index+1, "Books Name"] = bookNames
			(self.book_data).loc[index+1, "Sno"] = index+2
			(self.book_data).loc[index+1, "Total Book"] = noOfBooks
			(self.book_data).to_excel("Books_data.xls",index = False)
			print("======== Successfully Add Book In Library ========") 

		except ValueError:
			print("======== Please Enter Number Of Books   Not Allow String ========")	
		
				
	# Add New Student in Library
	def addStudent(self):
		count =0
		try:
			rollNo = int(input("Enter The Student Roll No :  ")) 
			name = input("Enter The Student Names : ")
			for index, item in (self.student_data).iterrows():
				count = index
			(self.student_data).loc[index+1, "Roll No"] = rollNo
			(self.student_data).loc[index+1, "Name"] = name
			(self.student_data).loc[index+1, "Sno"] = index+2
			(self.student_data).to_excel("Student_data.xls",index = False)
			print("======== Successfully Add Student In Library Data Base ========") 

		except ValueError:
			print("========= Please Enter Roll No.  Not Allow String ==========")	
	



# Class Rename (Student Data & Book Data) 
class rename:
	def __init__(self, bookData, studentData):
		self.book_data = bookData
		self.student_data = studentData
		
	#  Book Rename Update Function		
	def bookReName(self,bookName):
		if str(bookName).lower() != "none":
			try:
				choiceScreen='''Change Data ...................?\n
				  1. No Of Books
				  2. Book Name'''
				print(choiceScreen)
				print ("---------------------------------------------------------")
				choice = int(input("Enter Your Choice : "))
				if choice == 1:
				  	data = int(input("Enter The Update No Of Book : "))
				  	update = "No Of Books"
				  	temp = self.updateData(bookName,data,update) 
				  	if temp < data:
				  		for index, item in (self.book_data).iterrows():
				  			if str(item['Books Name']) == str(bookName):
				  				(self.book_data).loc[index, "Total Book"] = data
				  				(self.book_data).to_excel("Books_data.xls",index = False)
				  				
			
				elif choice == 2:
				  	data = input("Enter The Update Book Name : ")
				  	update = "Books Name"
				  	self.updateData(bookName, data, update)
				  	
				else:
				  	print ("---------------------------------------------------------")
				  	print("Please Enter Vaild Choice ")			  		  							  		 							 						
			except ValueError:
				print ("---------------------------------------------------------")
				print("Not Allow String in Number Of Books Block")			  		  			
		else:
			print("This Location Not Register Any Book. Please Try Again With Right Index Book")		


#  Update Book Name and Number of Books Function
	def updateData(self, bookName, Data, update):
		for index, item in (self.book_data).iterrows():
			if str(item['Books Name']) == str(bookName):
				(self.book_data).loc[index, f"{update}"] = Data
				(self.book_data).to_excel("Books_data.xls",index = False)
				print ("---------------------------------------------------------")
				print("Data Successfully Updated")
				print ("---------------------------------------------------------")
				temp = item['Total Book']
				return temp
		
				  													  											
# Student Data Upadte Function							
	def studentReName(self):
			try:
				choiceScreen='''Change Data ....................?\n
				  1. Student Roll No
				  2. Student Name'''
				print(choiceScreen)
				print ("---------------------------------------------------------")
				choice = int(input("Enter Your Choice : "))
				if choice == 1:
				  	data = int(input("Enter The Correction Student Roll No : "))
				  	last = input("Enter The Right Name : ")
				  	update = "Roll No"
				  	self.updateDataStudent(last,data,update) 		  			
				elif choice == 2:
				  	data = input("Enter The Correction Student Name : ")
				  	last = input("Enter The Right Roll No.  : ")
				  	update = "Name"
				  	self.updateDataStudent(last,data, update)
				  	
				else:
				  	print ("---------------------------------------------------------")
				  	print("Please Enter Vaild Choice ")			  		  							  		 							 						
			except ValueError:
				print ("---------------------------------------------------------")
				print("Not Allow String in Number Of Books Block")			  		  				


#  Student Data update Function (Name, Roll No)
	def updateDataStudent(self, lastData, Data, update):
		for index, item in (self.student_data).iterrows():
			if  str(item['Name']).lower() == str(lastData).lower()  or str(item['Roll No']) == str(lastData):
				(self.student_data).loc[index, f"{update}"] = Data
				(self.student_data).to_excel("Student_data.xls",index = False)
				print ("---------------------------------------------------------")
				print("Data Successfully Updated")
				print ("---------------------------------------------------------")
				return 0
				  											
			

	

		
	#  Main Function
if __name__=="__main__":
  book_data = pd.read_excel("Books_data.xls")
  student_data = pd.read_excel("Student_data.xls")
  initial = library(book_data, student_data) 
  student = Student (student_data,book_data)
  showData = StudentInfo(student_data)
  newData = NewDataAdd(student_data, book_data)
  reName = rename(book_data, student_data) 
  
  while(True):
      book_data = pd.read_excel("Books_data.xls")
      student_imdex =[]
      bookNo =[]
      menuDisplay = '''========================= MENU =========================
      1. Display Books
      2. Issue Books
      3. Return Books
      4. Show All Student Data
      5. Add New Books In Library
      6. Add New Student 
      7. Book Data Change (No Of Books / Books Name)
      8. Student Data Change (Name / Roll No )
      9. Exit'''
      print(menuDisplay)
      try:
      	choice = int(input("Enter Your Choise : "))
      	if choice == 1:
      		initial.display()
      		
      	elif choice == 2:
      		temp= initial.requestBook()
      		if str(temp).lower() != "":
      			student.issueBookStudent(temp)
      		else:
      			print("---------------------------------------------------------------")
      			print("All Book Issue At Time. Please Issue Book After The Student  Return The Books") 
    
      	elif choice == 3:
      		initial.returnBook(student.returnBookStudent()) 
      
      	elif choice == 4:
      		showData.display()
      	
      	elif choice ==5:
      		newData.addBooks()
      		
      	elif choice ==6:
      		newData.addStudent()
      
      	elif choice == 7:
      		reName.bookReName(initial.requestBook())
             					      	
      	elif choice == 8:
      		reName.studentReName()
            	     					
      	elif choice == 9:
      		print("==== Thanks for Using These Application ====\n")
      		exit() 
  
      	else:
      		print("====== Please Enter Vaild Choice ======\n")
    
      except ValueError:
      	print("** Enter The Vaild Number Not String Allow **\n")
		
      except TypeError:
      	continue	
      	
      if os.name == 'posix':
      	print ("---------------------------------------------------------")
      	input("Press The Enter Key For Continue")
      	_ = os.system('clear')		
      
  
       	
