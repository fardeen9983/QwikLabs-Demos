# Datastore
## Tasks
* Query data amd store it in Google Datastore using GCP

## Steps
### Store data
1. In left menu on the Console, Storage section, go to Datastore > Entities.
2. Under the Datastore mode column, click Select Datastore Mode.
3. Now choose where you'll create your database. Use the dropdown menu to select a location
   
    The location applies to both Cloud Datastore and App Engine for your Google Cloud Platform project. You cannot change the location after it has been saved.
4. Click Create database.

5. Click Create Entity.

6. On the Create an entity page, use [default] for Namespace.

7. Type Task for Kind.

8. Under Properties use the Add property button to add these properties, and click Done after each one:
   
    Name|Type|Value|Indexed
    -|-|-|-
    description|String|Learn Google Cloud Datastore|✕
    created|Date and time|(today's date)|✓
    done|Boolean|False|✓

1. Click Create. The console displays the Task entity that you just created.

### **Run a query**
Cloud Datastore supports querying data by kind or by Google Query Language (GQL); the instructions below walk you through the steps of doing both.

**Run kind queries**
1. Click Query by kind.
2. Select Task as the kind.

The query results show the Task entity that you created.

Next, add a query filter to restrict the results to entities that meet specific criteria:

1. Click Filter entities tab.

2. In the dropdown lists, select done, is a boolean, and that is false.

3. Click Apply filters. 
    The results show the Task entity that you created, since its done value is false.

4. Now try a query of done, is a boolean, and that is true then Apply filters. The results do not include the Task entity that you created, because its done value is not true.

### **Run GQL queries**
1. Click the Query by GQL tab.

2. In the query box add the following:
    ```sql
    SELECT * FROM Task
    ```
    Note that Task is case sensitive.

3. Click Run query.

    The query results show the Task entity that you created.

    Tip: The GQL query editor supports autocompletion for kinds: When you need to type a kind name, press Ctrl+Space to see a list of the available kinds. Up to 300 alphabetically sorted kinds can appear in the list. For better matches of kinds, type one or more characters.
4. Now add a query filter to restrict the results to entities that meet specific criteria:
    ```sql
    SELECT * FROM Task WHERE done=false
    ```