# mcp-openai-qwen-example

## Run

Run the following command

```bash
git clone https://github.com/skyer9/mcp-openai-qwen-example.git
cd mcp-openai-qwen-example

python -m venv venv

# Linux/Mac/WSL
source venv/bin/activate
# Window
# venv\Scripts\activate

pip install openai mcp

python mcp_openai_qwen_agent.py
```

```bash
Enter your prompt (or 'quit' to exit): insert data 200 to table tbl_test on column id.

Response: Great! The data `200` has been successfully inserted into the `tbl_test` table under the `id` column. If you need to insert more data or perform any other operations, feel free to let me know! I'm here to help.

Enter your prompt (or 'quit' to exit): list data of table tbl_test.

Response: Sure, here is the data from `tbl_test`:

- ID: 100
- ID: 200

Is there anything else you'd like to do with this table or any other information you need? Let me know how I can assist further!
```

## Verbose

Print all communications.

```bash
[SYSTEM] Starting MCP client...
[SYSTEM] Available tools: ['read_query', 'write_query', 'create_table', 'list_tables', 'describe_table', 'append_insight']
[SYSTEM] MCP client successfully initialized

Enter your prompt (or 'quit' to exit): list tables in database.
[USER INPUT] list tables in database.

[MODEL INPUT]
  system: You are a helpful assistant capable of accessing external functions and engaging in casual chat. Use...
  user: list tables in database.
  tools: ['read_query', 'write_query', 'create_table', 'describe_table', 'append_insight']

[MODEL OUTPUT]
  content:
  tool_calls: [ChatCompletionMessageToolCall(id='call_s54x4tgp', function=Function(arguments='{"query":"SELECT name FROM sqlite_mast                                                                                                                                                                                        er WHERE type=\'table\';"}', name='read_query'), type='function', index=0)]

[TOOL INPUT] read_query: {
  "query": "SELECT name FROM sqlite_master WHERE type='table';"
}
[TOOL OUTPUT] read_query: [{'name': 'tbl_test'}]

[MODEL INPUT WITH TOOL RESULTS]
  system: You are a helpful assistant capable of accessing external functions and engaging in casual chat. Use...
  user: list tables in database.
  assistant:
  tool: "[{'name': 'tbl_test'}]"

[MODEL FINAL OUTPUT]
  content: Great! It looks like there's one table in your database named **`tbl_test`**.

Would you like to see more details about this table, such as its columns and their data types? You can do that by describing the tab                                                                                                                                                                                        le. Just let me know how you'd like to proceed!

Response: Great! It looks like there's one table in your database named **`tbl_test`**.

Would you like to see more details about this table, such as its columns and their data types? You can do that by describing the tab                                                                                                                                                                                        le. Just let me know how you'd like to proceed!

Enter your prompt (or 'quit' to exit): quit
```