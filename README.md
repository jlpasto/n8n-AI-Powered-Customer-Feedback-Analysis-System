# AI-Powered Customer Feedback Analysis System using N8N

## 📝 Description

This n8n workflow automates the process of collecting, analyzing, and routing customer feedback. It's designed to streamline a company's response to customer inquiries by using AI to instantly classify feedback, ensuring the right department receives the right information quickly. This reduces manual effort, improves response times, and helps teams prioritize issues and feature requests more effectively.

-----

## 📖 Case Study

A company was struggling to manage the high volume of customer feedback it received daily. The feedback was submitted through a general contact form, and an employee had to manually read each submission, determine its purpose, and forward it to the appropriate team. This process was slow, error-prone, and caused significant delays.

The **AI-Powered Customer Feedback Analysis System** was implemented to solve this problem. Now, when a customer submits feedback, the system automatically processes it, identifies the sentiment and category, and routes it to the correct department without any human intervention. It also provides the customer with an immediate confirmation, complete with a tracking ID.

-----

## 🎯 Objective

The main objectives of this workflow are to:

  * **Automate feedback intake**: Automatically capture feedback from a web form.
  * **Analyze feedback**: Use an AI model to classify each piece of feedback by **sentiment** (Positive, Negative, Neutral) and **category** (Bug Report, Feature Request, Billing Issue, Praise, or General Inquiry).
  * **Centralize data**: Store all feedback, along with the AI's analysis, in a central database (Supabase) and a Google Sheet for easy access and reporting.
  * **Intelligent routing**: Automatically route feedback to the relevant internal teams based on its category.
  * **Enhance customer experience**: Provide customers with an immediate, automated response that includes a unique tracking ID.

-----

## 🧠 Workflow Breakdown

The workflow is triggered by a **Form Webhook** and progresses through the following steps:

1.  **Receive Feedback**: A webhook node listens for new submissions from a customer feedback form.
2.  **Parse Data**: A "Parse Response" **Code** node  extracts the customer's name, email, and feedback message from the raw webhook payload.
3.  **AI Analysis**: The "Feedback Analysis" **OpenAI** node  sends the feedback message to a ChatGPT-4o model. It's instructed to return a JSON object containing the `sentiment` and `category` of the feedback.
4.  **Process AI Output**: Another "Parse Response" **Code** node parses the AI's JSON output. It also generates a unique `feedback_id` and combines all the data (original feedback, AI analysis, and the new ID) into a single object.
5.  **Data Storage**:
      * A "Create a row" **Supabase** node saves the feedback to a `customer_feedback` table.
      * An "Append row in sheet" **Google Sheets** node adds the same data to a "Live Customer Feedback" spreadsheet for easy viewing.
6.  **Intelligent Routing**: A **Switch** node examines the `category` field from the AI analysis and routes the workflow to one of three branches:
      * **Feature Request**: Sends an email to the Product Team.
      * **Bug Report**: Sends an email to the IT Department.
      * **General Inquiry**: Sends an email to the Customer Service Team.
7.  **Customer Confirmation**: A "Send message to customer" **Gmail** node sends an automated confirmation email to the customer, thanking them for their feedback and providing the unique `feedback_id` for reference.

-----

## 🔧 Technical Highlights

  * **Webhook Trigger**: The workflow is event-driven, initiated by a POST request to a dedicated webhook URL.
  * **AI Integration**: Utilizes the **OpenAI** node to perform sentiment and category analysis using the `chatgpt-4o-latest` model.
  * **Custom Code**: **Code** nodes are used for custom data manipulation, including parsing the webhook payload, generating a unique ID (`FB-Timestamp-RandomString`), and handling potential AI response errors with a try-catch block.
  * **Data Persistence**: Integrates with **Supabase** for structured, long-term data storage and **Google Sheets** for a user-friendly, real-time log.
  * **Conditional Logic**: A **Switch** node provides powerful conditional routing, allowing for dynamic next steps based on the data's content.

-----

## 📂 File Structure
```cmd
/n8n-AI-Powered-Customer-Feedback-Analysis-System
│── README.md
│── AI-Powered Customer Feedback Analysis System.json # Exported n8n workflow
│── Flow Preview.png # Workflow preview
```

-----

## 🛠 Setup & Deployment

1.  **Import**: Import the `AI-Powered Customer Feedback Analysis System.json` file into your n8n instance.
2.  **Credentials**: You will need to configure the following credentials:
      * **Supabase**: An account to connect to your Supabase project.
      * **Google Sheets**: An account with access to the specified Google Sheet (`Live Customer Feedback`).
      * **OpenAI**: An API key to use the ChatGPT model.
      * **Gmail**: An account to send confirmation emails to customers and internal notifications.
3.  **Webhook**: The workflow's webhook URL will be automatically generated. You must configure your feedback form to send its submissions to this URL via a POST request.
4.  **Activation**: Activate the workflow by toggling the "Active" switch in the n8n editor.

-----

## 📌 Conclusion

This AI-powered workflow transforms a standard customer feedback process into an efficient, automated system. By leveraging AI for intelligent analysis and n8n for seamless integration and routing, it significantly improves operational efficiency and ensures customer feedback is addressed promptly by the right team. This leads to better customer satisfaction and more informed business decisions.

-----


## 📞 Contact
**Developer:** Jhon Loyd Pastorin  
**Email:** [jhonloydpastorin.03@gmail.com](mailto:jhonloydpastorin.03@gmail.com)  
**LinkedIn:** [Jhon Loyd Pastorin](www.linkedin.com/in/jhon-loyd-pastorin-a84000107)  
**Portfolio:** [jlpasto-portfolio.vercel.app](https://jlpasto-portfolio.vercel.app)  

-----
