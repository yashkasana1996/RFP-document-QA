# 🤖 RFP Document Q&A — Claude AI Application
### Natural Language Interface for Tender Document Analysis | Built on Anthropic Claude API

![Status](https://img.shields.io/badge/Status-Built%20%26%20Deployed-brightgreen)
![API](https://img.shields.io/badge/API-Anthropic%20Claude-orange)
![Type](https://img.shields.io/badge/Type-Web%20Application-blue)
![Use Case](https://img.shields.io/badge/Use%20Case-Enterprise%20Document%20Analysis-grey)

---

## 🔍 Problem Statement

Large corporations receive RFP (Request for Proposal) and tender documents that are 30–150 pages long. Bid teams spend significant time manually reading, extracting, and understanding:

- Scope of work and technical specifications
- Commercial terms, payment milestones, penalty clauses
- Submission requirements and deadlines
- Eligibility criteria and mandatory qualifications
- Risk and liability provisions

This manual process is slow, error-prone, and creates inconsistency across the estimation team. A senior estimator and a junior one will extract different information from the same document.

---

## 💡 Solution

A web application that allows any team member to **upload an RFP document and ask natural language questions** — getting instant, accurate answers sourced directly from the document text.

Built as a teaching vehicle for LLM application development using the Anthropic Claude API, this project demonstrates real enterprise value with minimal code.

---

## ✨ Features

- 📄 **Multi-format document support** — PDF, Word (.docx), Excel (.xlsx), plain text
- 💬 **Natural language Q&A** — Ask questions in plain English, get answers with document references
- 🔍 **Contextual responses** — Claude cites which section of the document the answer comes from
- 📋 **Auto-summary** — One-click executive summary of the entire document
- ⚠️ **Risk extraction** — Automatically surfaces penalty clauses, LDs, and liability provisions
- 📝 **Submission checklist** — Extracts and lists all required bid submission documents
- 🔄 **Multi-document comparison** — Compare two RFPs side by side for scope differences

---

## 🛠️ Tech Stack

```
Frontend:     HTML / CSS / JavaScript (vanilla — no framework)
AI Engine:    Anthropic Claude API (claude-sonnet-4-6)
PDF Parsing:  pdf.js (Mozilla)
Word Parsing: mammoth.js
Excel Import: SheetJS (xlsx)
Hosting:      Static HTML — deployable on GitHub Pages, Vercel, or Netlify
```

---

## 🏛️ Architecture

```
User Interface (Browser)
│
├── Document Upload
│   ├── PDF → pdf.js → raw text
│   ├── Word → mammoth.js → raw text
│   └── Excel → SheetJS → structured text
│
├── Text Processing
│   ├── Chunk document into context windows
│   ├── Build system prompt with document context
│   └── Maintain conversation history
│
└── Claude API (Anthropic)
    ├── System prompt: "You are an expert tender analyst..."
    ├── User message: question + document context
    └── Response: answer with document citation
```

---

## 💻 Core Code — API Call

```javascript
async function askClaude(question, documentText) {
  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "x-api-key": API_KEY,
      "anthropic-version": "2023-06-01"
    },
    body: JSON.stringify({
      model: "claude-sonnet-4-6",
      max_tokens: 1024,
      system: `You are an expert tender and RFP analyst with deep knowledge of 
               construction, interior fit-out, and corporate real estate contracts. 
               Analyse the following document and answer questions accurately, 
               citing the relevant section when possible.
               
               DOCUMENT:
               ${documentText}`,
      messages: [
        { role: "user", content: question }
      ]
    })
  });

  const data = await response.json();
  return data.content[0].text;
}
```

---

## 📊 Sample Q&A Interactions

**Input document:** 85-page corporate office fit-out RFP from a Fortune 500 client

**Q: "What is the project completion deadline?"**
> A: The project completion deadline is 16 weeks from the date of Purchase Order (PO) issuance, as stated in Section 4.2 (Project Timeline). An intermediate milestone of shell & core completion is set at Week 8.

**Q: "What are the liquidated damages provisions?"**
> A: Liquidated damages are specified in Clause 12.3 at ₹50,000 per day of delay beyond the contractual completion date, capped at 10% of the total contract value. The client reserves the right to terminate the contract if delay exceeds 4 weeks beyond the cap.

**Q: "List all documents required for bid submission"**
> A: Per Section 6.1, the following documents are mandatory with the bid submission:
> 1. Technical proposal (format as per Annexure A)
> 2. Commercial proposal (sealed, separate envelope)
> 3. Company registration certificate
> 4. Last 3 years audited financial statements
> 5. PAN and GST registration
> 6. EMD (Earnest Money Deposit) — ₹5,00,000 via DD
> 7. Portfolio of minimum 3 similar projects (>10,000 sq. ft.)

---

## 🎯 Enterprise Use Case Demonstrated

This application was built to solve a real problem in the ANJ Group contracts team — and demonstrates the core FDE skill: **identifying where AI creates specific, measurable business value, then building and deploying the tool.**

The pattern demonstrated here — document upload → Claude API → structured Q&A — is directly applicable to:
- Legal contract review
- Financial report analysis
- Policy document interpretation
- Medical records summarisation
- Regulatory compliance checking

---

## 🚀 How to Deploy (5 minutes)

1. Clone this repository
2. Add your Anthropic API key to `config.js`
3. Open `index.html` in any browser
4. Upload an RFP document and start asking questions

No server required. Runs entirely in the browser.

```bash
git clone https://github.com/yashwant-gurjar/rfp-document-qa
cd rfp-document-qa
# Add your API key to config.js
open index.html
```

---

## 📁 Repository Structure

```
rfp-document-qa/
├── README.md
├── index.html              ← Main application
├── config.js               ← API key configuration (gitignored)
├── config.example.js       ← Template for config
├── js/
│   ├── app.js              ← Main application logic
│   ├── claude-api.js       ← Anthropic API integration
│   ├── document-parser.js  ← PDF/Word/Excel parsing
│   └── ui.js               ← Interface interactions
├── css/
│   └── styles.css
└── docs/
    ├── screenshot-upload.png
    ├── screenshot-qa.png
    └── demo-video-link.md
```

---

## 🧠 What This Project Demonstrates

| Skill | How It's Demonstrated |
|---|---|
| Claude API integration | Direct API calls with system prompts and conversation history |
| Prompt engineering | Structured system prompts for domain-specific accuracy |
| Document processing | Multi-format parsing with pdf.js, mammoth, SheetJS |
| Enterprise problem-solving | Real business use case, not a tutorial project |
| Deployment thinking | Static HTML — no backend, no DevOps, instant deployment |

---

## 👤 Builder

**Yashwant Kumar Gurjar** — Strategy & AI Operations | Founder's Office | Digital Transformation
📞 +91 75970 92148 | 📧 yashkasana6991@gmail.com
🔗 [LinkedIn](https://linkedin.com/in/yashwant-gurjar96)
