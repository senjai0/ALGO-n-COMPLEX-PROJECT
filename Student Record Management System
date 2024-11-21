import streamlit as st

# Initialize the student records database
if "students" not in st.session_state:
    st.session_state["students"] = []

# Helper functions
def add_student(student):
    st.session_state["students"].append(student)

def update_student(index, updated_student):
    st.session_state["students"][index] = updated_student

def delete_student(index):
    st.session_state["students"].pop(index)

def search_student(name):
    return [student for student in st.session_state["students"] if name.lower() in student["name"].lower()]

def sort_students_by_key(key):
    st.session_state["students"].sort(key=lambda x: x[key])

# Streamlit UI
st.title("Student Record Management System")

menu = ["Create", "Read", "Update", "Delete", "Search", "Sort"]
choice = st.sidebar.selectbox("Select Operation", menu)

if choice == "Create":
    st.header("Add Student Record")
    name = st.text_input("Name")
    age = st.number_input("Age", min_value=0, step=1)
    gpa = st.number_input("GPA", min_value=0.0, max_value=4.0, step=0.1)
    if st.button("Add"):
        add_student({"name": name, "age": age, "gpa": gpa})
        st.success(f"Student {name} added successfully!")

elif choice == "Read":
    st.header("Student Records")
    if st.session_state["students"]:
        for i, student in enumerate(st.session_state["students"]):
            st.write(f"**{i + 1}. {student['name']}** - Age: {student['age']}, GPA: {student['gpa']}")
    else:
        st.info("No records available.")

elif choice == "Update":
    st.header("Update Student Record")
    if st.session_state["students"]:
        index = st.selectbox("Select Record to Update", range(len(st.session_state["students"])))
        student = st.session_state["students"][index]
        name = st.text_input("Name", student["name"])
        age = st.number_input("Age", min_value=0, step=1, value=student["age"])
        gpa = st.number_input("GPA", min_value=0.0, max_value=4.0, step=0.1, value=student["gpa"])
        if st.button("Update"):
            update_student(index, {"name": name, "age": age, "gpa": gpa})
            st.success(f"Student record updated successfully!")
    else:
        st.info("No records available.")

elif choice == "Delete":
    st.header("Delete Student Record")
    if st.session_state["students"]:
        index = st.selectbox("Select Record to Delete", range(len(st.session_state["students"])))
        if st.button("Delete"):
            delete_student(index)
            st.success("Student record deleted successfully!")
    else:
        st.info("No records available.")

elif choice == "Search":
    st.header("Search Student Record")
    name = st.text_input("Enter name to search")
    if st.button("Search"):
        results = search_student(name)
        if results:
            for student in results:
                st.write(f"**{student['name']}** - Age: {student['age']}, GPA: {student['gpa']}")
        else:
            st.warning("No matching records found.")

elif choice == "Sort":
    st.header("Sort Student Records")
    sort_by = st.selectbox("Sort By", ["name", "age", "gpa"])
    if st.button("Sort"):
        sort_students_by_key(sort_by)
        st.success(f"Records sorted by {sort_by} successfully!")
