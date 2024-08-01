# pitbit.ai_assignment
Here’s a simple Python script that can take a resume (as plain text input) and convert it into a structured JSON format. This is an example, and you may need to customize it further based on the specific structure of resumes you're working with.
# Prompt:

"Please take the content of the resume provided and convert it into a structured JSON format. The JSON should include the following fields: Name, Contact Information, Education, Skills, Work Experience, Projects, Certifications, Leadership, and Involvement. Each field should include relevant sub-fields where applicable, such as Degree, Institution, Year, etc. Ensure that the data is well-organized and accurately represents the resume's content."
### Script: `resume_parser.py`

```python
import json

def parse_resume(text):
    # Dummy data parsing; customize this function to fit the actual format of your resume.
    # Assume the text is in sections separated by newlines, for example.
    resume_data = {}

    # Splitting the text into sections by double newline
    sections = text.split("\n\n")

    # Parsing sections based on keywords (you may need to customize this)
    for section in sections:
        if "Name" in section:
            resume_data["Name"] = section.split(":")[1].strip()
        elif "Contact" in section:
            resume_data["Contact Information"] = {
                "Phone": section.split("Phone:")[1].split("\n")[0].strip(),
                "Email": section.split("Email:")[1].split("\n")[0].strip(),
                "Location": section.split("Location:")[1].split("\n")[0].strip()
            }
        elif "Education" in section:
            resume_data["Education"] = []
            education_entries = section.split("\n")[1:]
            for entry in education_entries:
                degree, institution, year, gpa = entry.split(", ")
                resume_data["Education"].append({
                    "Degree": degree.strip(),
                    "Institution": institution.strip(),
                    "Year": year.strip(),
                    "GPA": gpa.strip()
                })
        elif "Skills" in section:
            resume_data["Skills"] = section.split("Skills:")[1].strip().split(", ")
        elif "Work Experience" in section:
            resume_data["Work Experience"] = []
            work_entries = section.split("\n")[1:]
            for entry in work_entries:
                title, company, duration = entry.split(", ")
                resume_data["Work Experience"].append({
                    "Title": title.strip(),
                    "Company": company.strip(),
                    "Duration": duration.strip()
                })
        elif "Projects" in section:
            resume_data["Projects"] = []
            project_entries = section.split("\n")[1:]
            for entry in project_entries:
                name, description = entry.split(", ")
                resume_data["Projects"].append({
                    "Name": name.strip(),
                    "Description": description.strip()
                })
        elif "Certifications" in section:
            resume_data["Certifications"] = section.split("Certifications:")[1].strip().split(", ")
        elif "Leadership" in section:
            resume_data["Leadership"] = {
                "Position": section.split("Position:")[1].strip(),
                "Event": section.split("Event:")[1].strip(),
                "Impact": section.split("Impact:")[1].strip()
            }

    return json.dumps(resume_data, indent=4)

# Example usage
if __name__ == "__main__":
    resume_text = """
    Name: Saksham Kapadnis
    
    Contact Information:
    Phone: +91 7499198229
    Email: sakshamkapadnis.1@gmail.com
    Location: Pune, MH
    
    Education:
    Bachelor of Technology, Computer Engineering, BRACT’s Vishwakarma Institute of Information Technology, Pune, MH, 2021 - Present, 8.8
    Higher Secondary Examination, Ashoka Universal School & Matoshri College, Nasik, MH, 2019 - 2021, 95%
    
    Skills: Python, JavaScript, Java, C++, SQL, HTML, CSS, Node.js, ReactJS, Docker
    
    Work Experience:
    Software Engineer Intern, Thought Consulting Service, India, June 2023 - July 2023
    Software Engineer Intern, Oasis Infobyte, India, May 2023 - June 2023
    
    Projects:
    AI-Based Tool for Preliminary Diagnosis, Developed using Python and TensorFlow for Smart India Hackathon
    E-commerce Website, Developed using Bootstrap4, HTML5, and CSS with login authentication
    
    Certifications: Java Programming Fundamentals, Introduction to Data Science, Infosys Springboard
    
    Leadership:
    Position: Campaigning Team Lead
    Event: Annual college events
    Impact: Attracted over 5,000 visitors
    """

    parsed_resume = parse_resume(resume_text)
    print(parsed_resume)
```

### How the Script Works:
1. **Parsing the Resume**: The `parse_resume` function splits the resume text into sections based on double newlines, and then it checks each section for specific keywords to extract relevant information.

2. **JSON Output**: The extracted information is stored in a dictionary, which is then converted into a JSON string using `json.dumps`.

3. **Example Usage**: The script includes a block at the bottom that demonstrates how to use the `parse_resume` function with an example resume text.

### Next Steps:
- **Customize**: Modify the parsing logic to match the exact format of your resumes.
- **Test**: Run the script locally or in your preferred environment to ensure it works with actual resume data.
- **Upload to GitHub**: Follow the steps I provided earlier to create a GitHub repository, upload the script, and share the link.

This script is a starting point and can be expanded or refined based on your specific needs.
