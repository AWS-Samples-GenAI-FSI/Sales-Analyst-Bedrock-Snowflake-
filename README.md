# GenAI Sales Analyst
*(Powered by Amazon Bedrock and Snowflake)*

A powerful Streamlit application that transforms natural language questions into SQL queries and provides intelligent analysis of sales data using Amazon Bedrock, LangGraph, and FAISS vector search.

![Sales Analyst Demo](assets/images/demo.png)

## 🚀 Features

- **Natural Language to SQL**: Ask questions in plain English, get SQL queries automatically
- **Intelligent Analysis**: AI-powered insights and explanations of your data
- **Vector Search**: FAISS-powered semantic search for relevant database context
- **LangGraph Workflow**: Structured AI workflow with error handling and recovery
- **Real-time Monitoring**: Optional LangFuse integration for AI interaction tracking
- **Complete Automation**: Automatic database setup with Northwind sample data

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Streamlit UI  │───▶│  Amazon Bedrock  │───▶│   Snowflake     │
└─────────────────┘    └──────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│ FAISS Vector   │    │   LangGraph      │    │  Northwind      │
│ Store           │    │   Workflow       │    │  Database       │
└─────────────────┘    └──────────────────┘    └─────────────────┘
```

## 📋 Prerequisites

- **AWS Account** with Bedrock access
- **Snowflake Account** with appropriate permissions
- **Python 3.8+** installed
- **Git** (optional, for cloning)

## ⚡ Quick Start

### 1. Clone or Download
```bash
git clone https://github.com/AWS-Samples-GenAI-FSI/Sales-Analyst-Bedrock-Snowflake-.git
cd Sales-Analyst-Bedrock-Snowflake-
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure Credentials
```bash
cp .env.example .env
# Edit .env with your credentials
```

**Required Environment Variables:**
```bash
# AWS Configuration
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_access_key_here
AWS_SECRET_ACCESS_KEY=your_secret_key_here

# Snowflake Configuration
SNOWFLAKE_USER=your_username_here
SNOWFLAKE_PASSWORD=your_password_here
SNOWFLAKE_ACCOUNT=your_account_identifier_here
SNOWFLAKE_WAREHOUSE=COMPUTE_WH
SNOWFLAKE_ROLE=ACCOUNTADMIN
```

### 4. Run the Application
```bash
streamlit run app.py
```

### 5. Start Asking Questions!
The app will automatically:
- ✅ Connect to your Snowflake account
- ✅ Create the Northwind sample database
- ✅ Load complete dataset with relationships
- ✅ Initialize AI components
- ✅ Ready for natural language queries!

## 💬 Example Questions

### Basic Queries
- "What are the top 5 customers by order value?"
- "Count the number of orders by country"
- "Show me all products in the Beverages category"

### Advanced Analytics
- "What's the average order value by customer?"
- "Which products are most popular this year?"
- "Show me sales trends by month"
- "What's the distribution of order priorities?"

### Schema Exploration
- "Show me the schema of the CUSTOMERS table"
- "What columns are available in the ORDERS table?"
- "Describe the relationship between orders and customers"

## 📊 Sample Dataset

The application uses the complete **Northwind** dataset:

| Table | Records | Description |
|-------|---------|-------------|
| **CUSTOMERS** | 91 | Customer information and demographics |
| **ORDERS** | 830 | Order headers with dates and shipping |
| **ORDER_DETAILS** | 2,155 | Individual line items with quantities and prices |
| **PRODUCTS** | 77 | Product catalog with categories and pricing |
| **CATEGORIES** | 8 | Product categories and descriptions |
| **SUPPLIERS** | 29 | Supplier information and contacts |
| **EMPLOYEES** | 9 | Employee data and territories |
| **SHIPPERS** | 3 | Shipping company information |

## 🔧 Configuration Options

### AWS Bedrock Models
The application supports multiple Bedrock models:
- **Claude 3 Sonnet** (default) - Best balance of speed and accuracy
- **Claude 3 Haiku** - Fastest responses
- **Titan Text** - Cost-effective option

### Vector Search Settings
- **Embedding Model**: Amazon Titan Embeddings
- **Vector Dimensions**: 1536
- **Search Results**: Top 5 most relevant contexts

### Monitoring (Optional)
Enable LangFuse monitoring for AI interaction tracking:
```bash
LANGFUSE_PUBLIC_KEY=your_public_key
LANGFUSE_SECRET_KEY=your_secret_key
LANGFUSE_HOST=https://your-instance.langfuse.com
```

## 🛠️ Development

### Project Structure
```
├── app.py                    # Main Streamlit application
├── requirements.txt          # Python dependencies
├── .env.example             # Environment variables template
├── src/
│   ├── bedrock/             # Amazon Bedrock integration
│   ├── graph/               # LangGraph workflow components
│   ├── vector_store/        # FAISS vector search
│   ├── monitoring/          # LangFuse monitoring
│   ├── utils/               # Database connectors and utilities
│   └── prompts/             # AI prompt templates
└── assets/                  # Static assets and images
```

### Key Components

#### 1. Bedrock Helper (`src/bedrock/bedrock_helper.py`)
- Handles Amazon Bedrock API interactions
- Manages model selection and parameters
- Provides embedding generation

#### 2. LangGraph Workflow (`src/graph/workflow.py`)
- Structured AI workflow with error handling
- Query understanding and context retrieval
- SQL generation and result analysis

#### 3. Vector Store (`src/vector_store/faiss_manager.py`)
- FAISS-powered semantic search
- Database metadata indexing
- Context retrieval for SQL generation

#### 4. Snowflake Connector (`src/utils/snowflake_connector.py`)
- Database connection management
- Query execution and result formatting
- Schema introspection utilities

## 🔍 How It Works

### 1. Query Understanding
The AI analyzes your natural language question to understand:
- Intent (analysis, schema exploration, data retrieval)
- Required tables and columns
- Filters and aggregations needed

### 2. Context Retrieval
FAISS vector search finds relevant database metadata:
- Table schemas and relationships
- Column descriptions and sample values
- Previous successful query patterns

### 3. SQL Generation
Amazon Bedrock generates optimized SQL queries:
- Proper Snowflake syntax
- Efficient joins and aggregations
- Error handling and validation

### 4. Result Analysis
AI provides intelligent insights:
- Data interpretation and trends
- Business recommendations
- Explanations of findings

## 📈 Performance Tips

### Database Optimization
- Use appropriate Snowflake warehouse sizes
- Consider result caching for repeated queries
- Monitor query performance and costs

### AI Model Selection
- **Claude 3 Sonnet**: Best for complex analytical queries
- **Claude 3 Haiku**: Fastest for simple questions
- **Titan Text**: Most cost-effective for basic queries

### Vector Search Tuning
- Adjust similarity thresholds for better context
- Update metadata regularly for schema changes
- Use specific table/column descriptions

## 🚨 Troubleshooting

### Common Issues

**Connection Errors**
```bash
# Check Snowflake credentials
snowsql -a your_account -u your_username

# Verify AWS credentials
aws sts get-caller-identity
```

**SQL Generation Issues**
- Ensure proper table and column names in metadata
- Check for schema changes in your database
- Verify Bedrock model permissions

**Performance Issues**
- Increase Snowflake warehouse size
- Optimize vector search parameters
- Use query result caching

### Debug Mode
Enable detailed logging:
```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

## 💰 Cost Considerations

### AWS Bedrock
- **Claude 3 Sonnet**: ~$0.003 per 1K input tokens
- **Claude 3 Haiku**: ~$0.00025 per 1K input tokens
- **Titan Embeddings**: ~$0.0001 per 1K tokens

### Snowflake
- **Compute**: Based on warehouse size and usage time
- **Storage**: Based on data volume
- **Data Transfer**: Minimal for typical queries

**Estimated Monthly Cost**: $10-50 for moderate usage (100-500 queries)

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Setup
```bash
# Clone the repository
git clone https://github.com/AWS-Samples-GenAI-FSI/Sales-Analyst-Bedrock-Snowflake-.git

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install development dependencies
pip install -r requirements.txt
pip install -r requirements-dev.txt

# Run tests
pytest tests/
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/AWS-Samples-GenAI-FSI/Sales-Analyst-Bedrock-Snowflake-/issues)
- **Discussions**: [GitHub Discussions](https://github.com/AWS-Samples-GenAI-FSI/Sales-Analyst-Bedrock-Snowflake-/discussions)
- **AWS Support**: [AWS Support Center](https://console.aws.amazon.com/support/)

## 🏷️ Tags

`aws` `bedrock` `snowflake` `streamlit` `ai` `sql` `natural-language` `langraph` `faiss` `sales-analytics` `business-intelligence` `genai` `llm`

---

**Built with ❤️ by the AWS GenAI FSI Team**

*Transform your data analysis with the power of Generative AI!*
