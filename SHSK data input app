import streamlit as st
import random

# Function to generate a random 12-digit number starting with 1-9
def generate_school_id():
    return str(random.randint(1, 9)) + ''.join([str(random.randint(0, 9)) for _ in range(11)])

# Generate School ID and School Code
school_id = generate_school_id()
school_code = f"SHSK{school_id}"

# Streamlit form
with st.form("student_form"):
    title = st.text_input("Title")
    forename = st.text_input("Forename")
    surname = st.text_input("Surname")
    prename = st.text_input("PreName")
    nc_year = st.number_input("NC Year", min_value=1, max_value=13, step=1)
    enrolment_year = st.number_input("Enrolment School Year", min_value=2000, max_value=2100, step=1)
    enrolment_term = st.selectbox("Enrolment Term", options=["Michaelmas", "Lent", "Summer"])
    email_domain = "@abingdon.org.uk"
    email = f"{prename.lower()}.{surname.lower()}{email_domain}"
    home_email = st.text_input("Home Email Address")
    enrolment_date = st.date_input("Enrolment Date")
    enquiry_date = st.date_input("Enquiry Date")
    prospectus_enquiry_date = st.date_input("Prospectus Enquiry Date")
    
    # Submit button
    submitted = st.form_submit_button("Generate SQL")

# Generate SQL query
if submitted:
    official_name = f"{surname}, {forename}"
    full_name = f"{prename} {surname}"
    label_salutation = f"{title} {surname}"
    initials = prename[0] if prename else ''
    
    sql_query = f"""
    INSERT INTO tblPupilManagementPupils (
        txtSchoolID, txtSchoolCode, txtOfficialName, txtTitle, txtForename, txtSurname, 
        txtInitials, txtPreName, txtFullName, txtLabelSalutation, txtGender, intNCYear, 
        txtType, txtEmailAddress, txtHomeEmailAddress, txtEnrolmentDate, intEnrolmentSchoolYear, 
        intEnrolmentNCYear, txtEnrolmentTerm, txtEnquiryDate, txtAdmissionsStatus, 
        txtProspectusEnquiryDate, txtSubmitBy
    ) VALUES (
        '{school_id}', '{school_code}', '{official_name}', '{title}', '{forename}', '{surname}', 
        '{initials}', '{prename}', '{full_name}', '{label_salutation}', 'F', {nc_year}, 
        'SHSK', '{email}', '{home_email}', '{enrolment_date}', {enrolment_year}, 
        {nc_year}, '{enrolment_term}', '{enquiry_date}', 'Enrolled - SHSK', 
        '{prospectus_enquiry_date}', 'NID8235108017708803'
    );
    """
    
    st.code(sql_query, language='sql')
