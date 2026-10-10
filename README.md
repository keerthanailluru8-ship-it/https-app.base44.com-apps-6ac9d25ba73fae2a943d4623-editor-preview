from reportlab.lib.pagesizes import A4
from reportlab.lib import colors
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib.units import inch
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, PageBreak, ListFlowable, ListItem, Table, TableStyle
from pathlib import Path

pdf_path = Path("/mnt/data/ECE_CircuitMate_Mini_Project_Documentation.pdf")
project_url = "https://app.base44.com/apps/6ac9d25ba73fae2a943d4623/editor/preview"
styles = getSampleStyleSheet()
styles.add(ParagraphStyle(name="CTitle", parent=styles["Title"], fontName="Helvetica-Bold", fontSize=23, leading=28, alignment=1, textColor=colors.HexColor("#12345A"), spaceAfter=12))
styles.add(ParagraphStyle(name="CSub", parent=styles["Normal"], fontSize=12, leading=17, alignment=1, textColor=colors.HexColor("#247BA0"), spaceAfter=9))
styles.add(ParagraphStyle(name="CH1", parent=styles["Heading1"], fontSize=15, leading=19, textColor=colors.HexColor("#12345A"), spaceBefore=10, spaceAfter=6))
styles.add(ParagraphStyle(name="CH2", parent=styles["Heading2"], fontSize=11, leading=14, textColor=colors.HexColor("#247BA0"), spaceBefore=6, spaceAfter=3))
styles.add(ParagraphStyle(name="CB", parent=styles["BodyText"], fontSize=9.3, leading=13, spaceAfter=6))
styles.add(ParagraphStyle(name="CS", parent=styles["BodyText"], fontSize=8, leading=10, textColor=colors.HexColor("#444444"), spaceAfter=4))
def p(t, s="CB"): return Paragraph(t, styles[s])
def bl(items):
    return ListFlowable([ListItem(p(x)) for x in items], bulletType="bullet", leftIndent=18, bulletFontSize=8, spaceAfter=6)

story = [Spacer(1, 0.9*inch), p("MINI PROJECT DOCUMENTATION", "CSub"), Spacer(1, .15*inch),
         p("ECE CircuitMate", "CTitle"), p("AI Electronics Assistant", "CTitle"),
         p("An AI-assisted learning website for foundational electronics", "CSub"), Spacer(1, .3*inch)]
rows = [
    [p("<b>Project Title</b>"), p("ECE CircuitMate — AI Electronics Assistant")],
    [p("<b>Platform</b>"), p("Base44 AI App Builder")],
    [p("<b>Project Link</b>"), p(f'<link href="{project_url}" color="#247BA0">Open Base44 project preview</link>')],
    [p("<b>Student Name</b>"), p("________________________________")],
    [p("<b>Institution / Department</b>"), p("________________________________")],
    [p("<b>Academic Year</b>"), p("________________________________")],
]
t = Table(rows, colWidths=[1.7*inch, 4.4*inch], hAlign="CENTER")
t.setStyle(TableStyle([("BACKGROUND",(0,0),(0,-1),colors.HexColor("#EAF2F8")),("BOX",(0,0),(-1,-1),.6,colors.HexColor("#B8C9D9")),("INNERGRID",(0,0),(-1,-1),.35,colors.HexColor("#D5DFE8")),("VALIGN",(0,0),(-1,-1),"TOP"),("LEFTPADDING",(0,0),(-1,-1),8),("RIGHTPADDING",(0,0),(-1,-1),8),("TOPPADDING",(0,0),(-1,-1),8),("BOTTOMPADDING",(0,0),(-1,-1),8)]))
story += [t, Spacer(1,.5*inch), p("Prepared for academic submission and GitHub documentation","CSub"), PageBreak()]

def section(title, content):
    story.append(p(title, "CH1"))
    if isinstance(content, str): story.append(p(content))
    else: story.append(content)

section("Contents", bl(["1. Abstract","2. Introduction","3. Problem Statement","4. Objectives","5. Proposed Solution and Workflow","6. Main Modules","7. Innovation","8. Platform and Technology","9. Expected Outcomes","10. Limitations","11. Future Enhancements","12. Safety and Responsible Use","13. Conclusion","14. GitHub Publishing Checklist","15. References"]))
section("1. Abstract", "ECE CircuitMate is an educational web application concept designed to help Electronics and Communication Engineering (ECE) students learn foundational electronics in one place. It brings together component reference material, introductory circuit examples, guided calculations, troubleshooting suggestions, and quizzes. The project is created using Base44, an AI app-building platform that can generate application screens and workflows from natural-language instructions. Actual capabilities should be described according to the features implemented and tested in the project.")
section("2. Introduction", "Electronics is a core area of ECE. Beginners may need support to recognise electronic components, understand circuit behaviour, apply formulas, and investigate simple circuit issues. CircuitMate aims to make these learning tasks easier through a single, student-friendly website. It is a learning aid, not a replacement for laboratory instruction or instructor guidance.")
section("3. Problem Statement", "ECE students can find it challenging to understand circuit diagrams, identify electronic components, calculate circuit values, and troubleshoot basic electronics problems when immediate guidance is unavailable.")
section("4. Objectives", bl(["Present basic electronics concepts in beginner-friendly language.","Organise information about common electronic components.","Provide introductory circuit examples and explanations.","Support simple calculations using Ohm’s law (V = I × R).","Offer educational troubleshooting guidance.","Help students practise concepts through quizzes and feedback."]))
section("5. Proposed Solution and Workflow", "CircuitMate groups common introductory electronics learning activities into one web interface. A user chooses a module, reviews learning material or enters values into a calculator, and receives an explanation, result, or practice feedback. If an AI service is connected, the assistant may provide conversational answers. If no AI integration is configured, the assistant should be presented as a demonstration rather than a live AI feature.")
story.append(bl(["Open the project preview or published website.","Choose a section such as Components, Circuit Lab, Calculator, Assistant, or Quiz.","Review explanations, diagrams, or component details.","Enter valid values when using the calculator and check units.","Use quizzes to practise and review feedback."]))
section("6. Main Modules", "")
for h, d in [
    ("6.1 AI Electronics Assistant","A chat-style learning interface for electronics questions. Live answers depend on a correctly configured AI integration; demo content should be labelled clearly."),
    ("6.2 Component Library","Reference information for resistors, capacitors, diodes, LEDs, transistors, batteries, switches, and integrated circuits. Entries can explain symbols, functions, and common applications."),
    ("6.3 Circuit Learning Lab","Beginner circuit examples such as LED circuits, series and parallel circuits, and voltage dividers. Each example should include a diagram, component list, and working principle."),
    ("6.4 Ohm’s Law Calculator","Uses V = I × R to calculate voltage, current, or resistance when the other two values are supplied. Input validation and correct units are important."),
    ("6.5 Troubleshooting Guide","Provides possible causes and safe checks for common beginner issues. Suggestions are not a confirmed fault diagnosis."),
    ("6.6 Quiz and Progress","Multiple-choice practice with scores and explanations. Persistent progress tracking depends on the application's implemented storage features.")
]:
    story += [p(h,"CH2"), p(d)]
section("7. Innovation", "The project combines component learning, circuit examples, guided calculations, troubleshooting guidance, and quizzes in a single student-focused workflow. With a working AI integration, the assistant can add conversational explanations. The aim is to make foundational electronics practice more accessible and organised for learners.")
section("8. Platform and Technology", "The project is created using Base44 AI App Builder. Base44 describes its platform as supporting AI-generated application interfaces and workflows, with backend capabilities and publishing options. The exact framework, database, authentication, integrations, and AI model used by this specific project have not been independently verified for this report; list only technologies confirmed in the app’s configuration.")
story += [p('Base44 platform overview: <link href="https://base44.com/ai-app-builder" color="#247BA0">https://base44.com/ai-app-builder</link>',"CS"),
          p(f'Project preview: <link href="{project_url}" color="#247BA0">Open ECE CircuitMate</link>',"CS")]
section("9. Expected Outcomes", bl(["A central place to access beginner electronics learning resources.","A way to practise voltage, current, and resistance calculations.","More structured access to component references and circuit examples.","Self-checking through quizzes and feedback.","Safety-conscious initial troubleshooting guidance."]))
section("10. Limitations", bl(["Live AI answers require an active, correctly configured AI integration.","Interactive simulation is available only if a real simulator is implemented.","Troubleshooting suggestions cannot guarantee a diagnosis.","Technical content and component ratings should be checked against trusted course materials and datasheets.","Update this report to reflect the actual features tested."]))
section("11. Future Enhancements", bl(["Add circuit-image upload and component recognition using a suitable vision model.","Introduce an interactive circuit simulator.","Provide explanations in Telugu and other languages.","Add verified datasheet links and instructor-reviewed lessons.","Improve saved quiz scores and learning progress where supported."]))
section("12. Safety and Responsible Use", bl(["Disconnect power before changing circuit connections.","Do not experiment with mains or high-voltage circuits without qualified supervision.","Check component ratings and verify connections before powering a circuit.","Treat AI output as guidance; verify calculations and circuit advice using trusted material or an instructor."]))
section("13. Conclusion", "ECE CircuitMate aims to support ECE students as they build foundational electronics knowledge. By bringing component references, introductory circuit examples, calculations, troubleshooting guidance, and quizzes together, it provides a structured learning concept. Its value depends on the quality of the learning content and on which features are implemented and tested in the final application.")
section("14. GitHub Publishing Checklist", bl(["Upload this PDF to the GitHub repository, for example in a folder named docs/.","Add a README.md with the project overview, features, access instructions, and project link.","Add screenshots of the real application and identify which features are functional.","Confirm the exact technology stack and AI integrations before documenting them as implemented.","Remove secrets, private keys, and personal data from screenshots and repository files.","Test links, calculator inputs, quizzes, and other core features before submitting."]))
section("15. References", "")
story += [p('1. Base44, “AI App Builder.” <link href="https://base44.com/ai-app-builder" color="#247BA0">https://base44.com/ai-app-builder</link>',"CS"),
          p(f'2. ECE CircuitMate project preview supplied for this report: <link href="{project_url}" color="#247BA0">Open project</link>',"CS"),
          p("<b>Before final submission:</b> Add your name, institution, department, academic year, and screenshots. Verify the live application’s actual features and update this documentation accordingly.","CS")]

def footer(canvas, doc):
    canvas.saveState()
    w, h = A4
    canvas.setStrokeColor(colors.HexColor("#D5DFE8"))
    canvas.line(.65*inch,.55*inch,w-.65*inch,.55*inch)
    canvas.setFont("Helvetica",8); canvas.setFillColor(colors.HexColor("#5C6770"))
    canvas.drawString(.7*inch,.35*inch,"ECE CircuitMate — AI Electronics Assistant")
    canvas.drawRightString(w-.7*inch,.35*inch,f"Page {doc.page}")
    canvas.restoreState()

doc = SimpleDocTemplate(str(pdf_path), pagesize=A4, rightMargin=.7*inch, leftMargin=.7*inch, topMargin=.65*inch, bottomMargin=.75*inch, title="ECE CircuitMate — Mini Project Documentation", author="Project Team")
doc.build(story, onFirstPage=footer, onLaterPages=footer)
print(f"Created PDF: {pdf_path}")
