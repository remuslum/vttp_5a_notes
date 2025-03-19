---


---

<h1 id="paf">PAF</h1>
<h2 id="sql">SQL</h2>
<h3 id="configure-jdbc-connection-pool">Configure JDBC Connection Pool</h3>
<blockquote>
<p>spring.datasource.url=<br>
<strong>must start with jdbc</strong><br>
spring.datasource.username=<br>
spring.datasource.password=</p>
</blockquote>
<h3 id="making-queries-in-java">Making queries in Java</h3>
<blockquote>
<p>@Autowired<br>
private JdbcTemplate jdbcTemplate<br>
inject an instance of JdbcTemplate</p>
</blockquote>
<h3 id="create-users-and-grant-permissions">Create users and grant permissions</h3>
<ul>
<li>Creating users</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"> <span class="token keyword">CREATE</span> <span class="token keyword">USER</span> <span class="token string">"&lt;user_name&gt;"</span><span class="token variable">@"%"</span> IDENTIFIED <span class="token keyword">BY</span> <span class="token string">'&lt;password&gt;'</span>
</code></pre>
<ul>
<li>Granting permissions</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">GRANT</span> <span class="token keyword">ALL</span> <span class="token keyword">PRIVILEGES</span> <span class="token keyword">ON</span> <span class="token operator">&lt;</span>db_name<span class="token operator">&gt;</span> <span class="token keyword">TO</span> <span class="token string">'&lt;user_name&gt;'</span><span class="token variable">@'%'</span>
</code></pre>
<h3 id="create">Create</h3>
<ul>
<li>Database</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">CREATE</span> <span class="token keyword">DATABASE</span> <span class="token operator">&lt;</span>db_name<span class="token operator">&gt;</span>
</code></pre>
<ul>
<li>Table</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">CREATE</span> <span class="token keyword">TABLE</span> <span class="token operator">&lt;</span>table_name<span class="token operator">&gt;</span> <span class="token punctuation">(</span>
<span class="token operator">&lt;</span>column_name<span class="token operator">&gt;</span> <span class="token operator">&lt;</span>type_constraint<span class="token operator">&gt;</span><span class="token punctuation">)</span>
<span class="token keyword">CONSTRAINT</span> <span class="token operator">&lt;</span>constraint_name<span class="token operator">&gt;</span> <span class="token keyword">PRIMARY</span> <span class="token keyword">KEY</span> <span class="token punctuation">(</span><span class="token operator">&lt;</span>column_name<span class="token operator">&gt;</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Insert</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">INSERT</span> <span class="token keyword">INTO</span> <span class="token operator">&lt;</span>table_name<span class="token operator">&gt;</span> <span class="token keyword">VALUES</span> <span class="token punctuation">(</span>?<span class="token punctuation">,</span>?<span class="token punctuation">,</span>?<span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Insert (Java)</li>
</ul>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@Repository</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">TVShowRepository</span><span class="token punctuation">{</span>
	<span class="token annotation punctuation">@Autowired</span>
	<span class="token keyword">private</span> JdbcTemplate template<span class="token punctuation">;</span>

	<span class="token keyword">public</span> <span class="token keyword">boolean</span> <span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">final</span> TVShow tv<span class="token punctuation">)</span><span class="token punctuation">{</span>
		<span class="token keyword">int</span> added <span class="token operator">=</span> template<span class="token punctuation">.</span><span class="token function">update</span><span class="token punctuation">(</span>
		"INSERT INTO <span class="token function">tv_shows</span><span class="token punctuation">(</span>prog_id<span class="token punctuation">,</span>name<span class="token punctuation">,</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span> <span class="token function">VALUES</span> <span class="token punctuation">(</span><span class="token operator">?</span><span class="token punctuation">,</span><span class="token operator">?</span><span class="token punctuation">,</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
		<span class="token keyword">return</span> added <span class="token operator">&gt;</span> <span class="token number">0</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<ul>
<li>Batch Insert (Java)</li>
</ul>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@Repository</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">TVShowRepository</span> <span class="token punctuation">{</span>
	<span class="token annotation punctuation">@Autowired</span>
	<span class="token keyword">private</span> JdbcTemplate template<span class="token punctuation">;</span>

	<span class="token keyword">public</span> <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">final</span> List<span class="token operator">&lt;</span>TVShow<span class="token operator">&gt;</span> shows<span class="token punctuation">)</span><span class="token punctuation">{</span>
		<span class="token comment">// Cast to a list of object[] first</span>
		List<span class="token operator">&lt;</span>Object<span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span> params <span class="token operator">=</span> shows<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span>tv <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token keyword">new</span> <span class="token class-name">Object</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">{</span>tv<span class="token punctuation">.</span><span class="token function">getId</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> tv<span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span>

		<span class="token keyword">int</span> added<span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token operator">=</span> template<span class="token punctuation">.</span><span class="token function">updateBatch</span><span class="token punctuation">(</span><span class="token string">"INSERT INTO tv_shows(prog_id,name,...) VALUES (?,?,...)"</span><span class="token punctuation">,</span> params<span class="token punctuation">)</span>
		<span class="token keyword">return</span> added<span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Columns can skipped if they are ‘nullable’ or auto incremented</p>
<h3 id="read">Read</h3>
<ul>
<li>Read records (SQL) :</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">SELECT</span> <span class="token operator">&lt;</span>wanted_records<span class="token operator">&gt;</span> <span class="token keyword">FROM</span> <span class="token operator">&lt;</span>table_name<span class="token operator">&gt;</span>
<span class="token keyword">LIMIT</span> <span class="token operator">&lt;</span>number<span class="token operator">&gt;</span>
<span class="token keyword">WHERE</span> <span class="token operator">&lt;</span>predicate<span class="token operator">&gt;</span>
<span class="token operator">AND</span><span class="token punctuation">,</span><span class="token operator">OR</span><span class="token punctuation">,</span><span class="token operator">NOT</span> <span class="token operator">&lt;</span>predicate<span class="token operator">&gt;</span>
</code></pre>
<ul>
<li>Read records (Java):
<ul>
<li>SQL queries<br>
Use “?” as placeholder for values in prepared statement to construct query</li>
</ul>
</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql">	<span class="token keyword">SELECT</span> id <span class="token keyword">FROM</span> employees <span class="token keyword">WHERE</span> id <span class="token operator">=</span> ?
</code></pre>
<ul>
<li>Methods to get records in Java: query(), queryForRowSet(), queryForObject(), queryForList()
<ul>
<li><em>query()</em> : For complicated mapping to Java objects</li>
<li><em>queryForRowSet()</em> : To extract the rowSet</li>
<li><em>queryForObject()</em> : expects only one row</li>
<li><em>queryForList()</em>: For mapping to a List of objects of the same type, no need for RowMapper</li>
<li>2 ways to do: <em>lambda expression</em> <strong>OR</strong> defining a <em>new class</em> that <strong>implements</strong> RowMapper&lt;class_name&gt;</li>
</ul>
</li>
<li>Code block for RowMapper:</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyObjectRowMapper</span> <span class="token keyword">implements</span> <span class="token class-name">RowMapper</span><span class="token operator">&lt;</span>MyObject<span class="token operator">&gt;</span> <span class="token punctuation">{</span>
    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> MyObject <span class="token function">mapRow</span><span class="token punctuation">(</span>ResultSet rs<span class="token punctuation">,</span> <span class="token keyword">int</span> rowNum<span class="token punctuation">)</span> <span class="token keyword">throws</span> SQLException <span class="token punctuation">{</span>
        MyObject obj <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">MyObject</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        obj<span class="token punctuation">.</span><span class="token function">setId</span><span class="token punctuation">(</span>rs<span class="token punctuation">.</span><span class="token function">getInt</span><span class="token punctuation">(</span><span class="token string">"id"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        obj<span class="token punctuation">.</span><span class="token function">setName</span><span class="token punctuation">(</span>rs<span class="token punctuation">.</span><span class="token function">getString</span><span class="token punctuation">(</span><span class="token string">"name"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> obj<span class="token punctuation">;</span>
	    <span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
	List<span class="token operator">&lt;</span>MyObject<span class="token operator">&gt;</span> list <span class="token operator">=</span> jdbcTemplate<span class="token punctuation">.</span><span class="token function">query</span><span class="token punctuation">(</span><span class="token string">"SELECT * FROM my_table"</span><span class="token punctuation">,</span> <span class="token keyword">new</span> <span class="token class-name">MyObjectRowMapper</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<ul>
<li>
<p>query() example (used mainly for complex mapping):</p>
<ul>
<li>Using lambda function:</li>
</ul>
</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	List<span class="token operator">&lt;</span>MyObject<span class="token operator">&gt;</span> list <span class="token operator">=</span> jdbcTemplate<span class="token punctuation">.</span><span class="token function">query</span><span class="token punctuation">(</span><span class="token string">"SELECT * FROM my_table"</span><span class="token punctuation">,</span> 
	<span class="token punctuation">(</span>rs<span class="token punctuation">,</span> rowNum<span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token keyword">new</span> <span class="token class-name">MyObject</span><span class="token punctuation">(</span>rs<span class="token punctuation">.</span><span class="token function">getInt</span><span class="token punctuation">(</span><span class="token string">"id"</span><span class="token punctuation">)</span><span class="token punctuation">,</span> rs<span class="token punctuation">.</span><span class="token function">getString</span><span class="token punctuation">(</span><span class="token string">"name"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 
</code></pre>
<ul>
<li>Rowset:</li>
</ul>
<blockquote>
<p>Check if a row is present</p>
</blockquote>
<pre class=" language-java"><code class="prism  language-java">	rowSet<span class="token punctuation">.</span><span class="token function">first</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> returns a <span class="token keyword">boolean</span>
</code></pre>
<p><strong>Important</strong>: Wrap the get results with an Optional to prevent NullPointerException, especially if you are using SELECT with WHERE</p>
<h3 id="update">Update</h3>
<ul>
<li>Update a record (SQL) :</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">UPDATE</span> <span class="token operator">&lt;</span>table_name<span class="token operator">&gt;</span> <span class="token keyword">SET</span> <span class="token operator">&lt;</span>column_name<span class="token operator">&gt;</span> <span class="token operator">=</span> <span class="token operator">&lt;</span>new_value<span class="token operator">&gt;</span> <span class="token keyword">WHERE</span> <span class="token operator">&lt;</span>condition_column<span class="token operator">&gt;</span> <span class="token operator">=</span> <span class="token operator">&lt;</span>filtered_term<span class="token operator">&gt;</span>
</code></pre>
<p>Key point: <strong>Condition</strong> of the update must be <strong>present</strong></p>
<h3 id="delete">Delete</h3>
<ul>
<li>Delete a row (SQL) :</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">DELETE</span> <span class="token keyword">FROM</span> <span class="token operator">&lt;</span>table_name<span class="token operator">&gt;</span> <span class="token keyword">WHERE</span> <span class="token operator">&lt;</span>condition_column<span class="token operator">&gt;=</span><span class="token operator">&lt;</span>filtered_term<span class="token operator">&gt;</span>
</code></pre>
<p>Important: Must have <strong>condition</strong> in place</p>
<h3 id="cud-operations-in-java">CUD operations in Java</h3>
<ul>
<li>Use <strong>template.update</strong> to execute prepared update statements (insert, update, delete)</li>
</ul>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">int</span> added <span class="token operator">=</span> jdbcTemplate<span class="token punctuation">.</span><span class="token function">update</span><span class="token punctuation">(</span><span class="token string">"&lt;sql_statement&gt;"</span><span class="token punctuation">,</span> values<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span> 
<span class="token keyword">return</span> added <span class="token operator">&gt;</span> <span class="token number">0</span>
</code></pre>
<h3 id="aggregation">Aggregation</h3>
<ul>
<li>Perform calculations on a set of records and return a single value.</li>
<li>Less costly operation as it only returns one value</li>
<li>Functions like <strong>COUNT</strong> can be used to check if the database has records in it (Cheaper)</li>
<li>Such functions include <strong>SUM, COUNT, AVERAGE, MIN, MAX, DISTINCT, STDEV</strong></li>
<li>Aggregating by Category (<strong>GROUP BY</strong>) : the <strong>HAVING</strong> clause can be used instead of <strong>WHERE</strong> as aggregation does not allow <strong>WHERE</strong> operations.</li>
</ul>
<h3 id="window-functions">Window Functions</h3>
<ul>
<li>
<p>2 types of window functions:</p>
<ol>
<li>Aggregate</li>
<li>Analytical</li>
</ol>
</li>
<li>
<p><strong>PARTITION BY</strong> defines a window over a set of rows from the same table, used with the <strong>OVER</strong> clause</p>
</li>
<li>
<p>The result is the same number of records, with each record having an additional aggregation column.</p>
</li>
<li>
<p>This is commonly used when there is a need to compare each record against the aggregation column</p>
</li>
</ul>
<h2 id="relationship-cardinality">Relationship Cardinality</h2>
<p>Tables are related to one another via primary key and foreign key.</p>
<ul>
<li>One to one</li>
<li>One to many</li>
<li>Many to Many</li>
</ul>
<h3 id="foreign-key">Foreign Key</h3>
<ul>
<li>Foreign Key: A field in a table that references the primary key of another table</li>
<li>Referential integrity - foreign key constraint
<ul>
<li>Cannot delete a record if there are foreign keys referencing it</li>
<li>Cannot insert values in a foreign key field that are not present in the referencing primary key field</li>
<li>Do not have to be unique</li>
<li>Can be null even if the primary key field that it references is not</li>
<li>To modify the behaviour of foreign key, in the SQL file:</li>
</ul>
</li>
</ul>
<blockquote>
<p>Cascade: apply the action to all records that references the primary key as the foreign key</p>
</blockquote>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">constraint</span> fk_prog_id
	<span class="token keyword">foreign</span> <span class="token keyword">key</span><span class="token punctuation">(</span>prog_id<span class="token punctuation">)</span>
	<span class="token keyword">references</span> tv_shows<span class="token punctuation">(</span>prog_id<span class="token punctuation">)</span>
	<span class="token keyword">on</span> <span class="token keyword">delete</span> <span class="token keyword">cascade</span>
	<span class="token keyword">on</span> <span class="token keyword">update</span> <span class="token keyword">cascade</span>
</code></pre>
<blockquote>
<p>Set null: set the foreign key column to null when the parent key is deleted</p>
</blockquote>
<pre class=" language-sql"><code class="prism  language-sql">	<span class="token keyword">constraint</span> fk_prog_id
		<span class="token keyword">foreign</span> <span class="token keyword">key</span><span class="token punctuation">(</span>prog_id<span class="token punctuation">)</span>
		<span class="token keyword">references</span> tv_shows<span class="token punctuation">(</span>prog_id<span class="token punctuation">)</span>
		<span class="token keyword">on</span> <span class="token keyword">delete</span> <span class="token keyword">set</span> <span class="token boolean">null</span>
		<span class="token keyword">on</span> <span class="token keyword">update</span> <span class="token keyword">cascade</span>
</code></pre>
<h3 id="database-views">Database views</h3>
<ul>
<li>View is a table that is defined from one or more queries</li>
<li>The table is computed when it is accessed
<ul>
<li>No data are stored</li>
</ul>
</li>
<li>Views from a <strong>single query</strong> can be modified, while views derived from <strong>joins</strong> or <strong>aggregations</strong> CANNOT be modified.</li>
<li>Example:</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">CREATE</span> <span class="token keyword">VIEW</span> aug_shows <span class="token keyword">AS</span>
	<span class="token keyword">SELECT</span> <span class="token operator">*</span> <span class="token keyword">FROM</span> tv_shows tv <span class="token keyword">WHERE</span> tv<span class="token punctuation">.</span>release_date <span class="token operator">&gt;</span> <span class="token string">'2019-08-01'</span>
</code></pre>
<h3 id="normalization">Normalization</h3>
<ul>
<li>Systematic process of eliminating redundancy from the database</li>
<li>The result is eliminating redundancies and improve data integrity</li>
</ul>
<ol>
<li>First Normal Form
<ul>
<li>Every row must have an unique identifier, the primary key</li>
<li>The value in every column must be atomic</li>
</ul>
</li>
<li>Second Normal Form
<ul>
<li>In first normal form</li>
<li>Non prime columns must be dependent on the entire primary key</li>
</ul>
</li>
<li>Third Normal Form
<ul>
<li>Must be in second normal form</li>
<li>Non prime columns must be independent of one another</li>
</ul>
</li>
</ol>
<h3 id="subqueries">Subqueries</h3>
<ul>
<li>Queries within a query</li>
<li>The inner query must be a <strong>SELECT</strong> statement enclosed in parenthesis</li>
<li>The inner query can return
<ul>
<li>A single value</li>
<li>A single row</li>
<li>A table</li>
</ul>
</li>
</ul>
<h3 id="indexes">Indexes</h3>
<ul>
<li>Structures that improves data retrieval</li>
<li>Index is created automatically for primary key
<ul>
<li>Other columns are optional</li>
</ul>
</li>
<li>Indexes are useful for:
<ul>
<li>Reducing query time</li>
<li>Grouping</li>
<li>Sorting</li>
<li>Min and Max values</li>
</ul>
</li>
<li>For multi column index, the column with higher cardinality (more unique values) should be placed first</li>
</ul>
<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">CREATE</span> <span class="token keyword">INDEX</span> <span class="token operator">&lt;</span>idx_name<span class="token operator">&gt;</span> <span class="token keyword">ON</span> <span class="token operator">&lt;</span>table_name<span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token operator">&lt;</span>columns_name<span class="token operator">&gt;</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="transactions">Transactions</h3>
<ul>
<li>Group multiple operations into a single function (atomic of work)
<ul>
<li>All operations within this group must succeed or not performed at all</li>
<li>Keep the database in a consistent state</li>
</ul>
</li>
<li>At the end of a transaction
<ul>
<li>Commit - save all the work performed inside the transaction</li>
<li>Rollback - discard all the work performed inside the transaction</li>
</ul>
</li>
<li>When to use transaction?
<ul>
<li>When you have to modify related data from a few different tables from the same database</li>
<li>If any one of the operation fails, then must revert all the modified data back to its original value</li>
</ul>
</li>
<li>Performing Transaction
<ul>
<li>Methods that perform transaction are modified with <strong>@Transactional</strong></li>
<li>Transaction will rollback when an unchecked exception is thrown</li>
</ul>
</li>
</ul>
<h2 id="mongo">Mongo</h2>
<ul>
<li>Mongo is a document database.
<ul>
<li>A document is a JSON object.</li>
<li>All documents have a primary key annotated with “_id”. If primary key is not provided in document, it is automatically generated</li>
</ul>
</li>
</ul>
<h3 id="querying-mongo-in-java">Querying mongo in Java</h3>
<pre class=" language-java"><code class="prism  language-java">	<span class="token annotation punctuation">@Autowired</span>
	<span class="token keyword">private</span> MongoTemplate mongoTemplate
</code></pre>
<h3 id="create-documents-in-mongo">Create documents in Mongo</h3>
<ul>
<li>Shell</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.insert({...})
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	<span class="token annotation punctuation">@Autowired</span>
	<span class="token keyword">private</span> MongoTemplate mongoTemplate
	Document toInsert <span class="token operator">=</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token comment">// mongoTemplate.insert() returns a new Document</span>
	Document newDoc <span class="token operator">=</span> mongoTemplate<span class="token punctuation">.</span><span class="token function">insert</span><span class="token punctuation">(</span>toInsert<span class="token punctuation">,</span> <span class="token operator">&lt;</span>collection_name<span class="token operator">&gt;</span><span class="token punctuation">)</span>
	ObjectId id <span class="token operator">=</span> newDoc<span class="token punctuation">.</span><span class="token function">getObjectId</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	<span class="token comment">// Check if id is null or not to see if insert is valid</span>
	
	<span class="token comment">// Batch update</span>
	List<span class="token operator">&lt;</span>Document<span class="token operator">&gt;</span> docsToInsert <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">LinkedList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	<span class="token comment">// Add document to list</span>
	
	Collection<span class="token operator">&lt;</span>Document<span class="token operator">&gt;</span> newDocs <span class="token operator">=</span> mongoTemplate<span class="token punctuation">.</span><span class="token function">insert</span><span class="token punctuation">(</span>
		docsToInsert<span class="token punctuation">,</span> <span class="token operator">&lt;</span>collection_name<span class="token operator">&gt;</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="read-data-in-mongo">Read data in Mongo</h3>
<ul>
<li>Shell</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.find({...})
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	<span class="token annotation punctuation">@Autowired</span>
	<span class="token keyword">private</span> MongoTempate mongoTemplate<span class="token punctuation">;</span>
	<span class="token comment">// Define criteria to filter</span>
	Criteria criteria <span class="token operator">=</span> Criteria<span class="token punctuation">.</span><span class="token function">where</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">is</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">is</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	Query query <span class="token operator">=</span> Query<span class="token punctuation">.</span><span class="token function">query</span><span class="token punctuation">(</span>criteria<span class="token punctuation">)</span><span class="token punctuation">;</span>
	List<span class="token operator">&lt;</span>Document<span class="token operator">&gt;</span> result <span class="token operator">=</span> mongoTemplate<span class="token punctuation">.</span><span class="token function">find</span><span class="token punctuation">(</span>query<span class="token punctuation">,</span> Document<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> collection_name<span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Another alternative to multiple criterias</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	Criteria criteria <span class="token operator">=</span> Criteria<span class="token punctuation">.</span><span class="token function">andOperator</span><span class="token punctuation">(</span>
	Criteria<span class="token punctuation">.</span><span class="token function">where</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token function">regex</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
	Criteria<span class="token punctuation">.</span><span class="token function">where</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">is</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<ul>
<li>Find by ObjectId</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	<span class="token keyword">public</span> Optional<span class="token operator">&lt;</span>Document<span class="token operator">&gt;</span> <span class="token function">findTVShowById</span><span class="token punctuation">(</span>String <span class="token function">id</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
		ObjectId docId <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ObjectId</span><span class="token punctuation">(</span>id<span class="token punctuation">)</span><span class="token punctuation">;</span>
		<span class="token keyword">return</span> Optional<span class="token punctuation">.</span><span class="token function">ofNullable</span><span class="token punctuation">(</span>mongoTemplate<span class="token punctuation">.</span><span class="token function">findById</span><span class="token punctuation">(</span>docId<span class="token punctuation">,</span> Document<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> <span class="token operator">&lt;</span>collection_name<span class="token operator">&gt;</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<ul>
<li>Sort in Mongo</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	Query query <span class="token operator">=</span> Query<span class="token punctuation">.</span><span class="token function">query</span><span class="token punctuation">(</span>
		Criteria<span class="token punctuation">.</span><span class="token function">where</span><span class="token punctuation">(</span><span class="token string">"awards"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">exists</span><span class="token punctuation">(</span><span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">with</span><span class="token punctuation">(</span>
		Sort<span class="token punctuation">.</span><span class="token function">by</span><span class="token punctuation">(</span>Sort<span class="token punctuation">.</span>Direction<span class="token punctuation">.</span>ASC<span class="token punctuation">,</span> <span class="token string">"title"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="update-documents-in-mongo">Update documents in Mongo</h3>
<ul>
<li>Shell</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.updateOne(
		{&lt;column&gt;:&lt;value&gt;}, 
		{$set : {&lt;column&gt;:&lt;new_value&gt;}})
	// use update() to update all documents matching the predicate
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	Query query <span class="token operator">=</span> Query<span class="token punctuation">.</span><span class="token function">query</span><span class="token punctuation">(</span>Criteria<span class="token punctuation">.</span><span class="token function">where</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">is</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
	Update updateOps <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Update</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">set</span><span class="token punctuation">(</span><span class="token operator">&lt;</span>column_name<span class="token operator">&gt;</span><span class="token punctuation">,</span><span class="token operator">&lt;</span>value<span class="token operator">&gt;</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	UpdateResult updateResult <span class="token operator">=</span> mongoTemplate<span class="token punctuation">.</span><span class="token function">updateMulti</span><span class="token punctuation">(</span>query<span class="token punctuation">,</span>updateOps<span class="token punctuation">,</span> Document<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span><span class="token operator">&lt;</span>collection_name<span class="token operator">&gt;</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Upsert</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	<span class="token comment">// Same updateOps as update</span>
	UpdateResult updateResult <span class="token operator">=</span> mongoTemplate<span class="token punctuation">.</span><span class="token function">upsert</span><span class="token punctuation">(</span>query<span class="token punctuation">,</span> updateOps<span class="token punctuation">,</span> <span class="token operator">&lt;</span>collection_name<span class="token operator">&gt;</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="delete-documents-in-mongo">Delete documents in Mongo</h3>
<ul>
<li>Shell</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.deleteOne({...})
	db.&lt;collection_name&gt;.deleteMany({...})
</code></pre>
<ul>
<li>If deleteMany is empty, all documents will be deleted</li>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	Query query <span class="token operator">=</span> Query<span class="token punctuation">.</span><span class="token function">query</span><span class="token punctuation">(</span>Criteria<span class="token punctuation">.</span><span class="token function">where</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">exists</span><span class="token punctuation">(</span><span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token comment">// Mongo class DeleteResult is returned for remove()</span>
	DeleteResult result <span class="token operator">=</span> mongoTemplate<span class="token punctuation">.</span><span class="token function">remove</span><span class="token punctuation">(</span>query<span class="token punctuation">,</span> <span class="token operator">&lt;</span>collection_shows<span class="token operator">&gt;</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="indexes-1">Indexes</h3>
<ul>
<li>Like RDBMS, indexes are used by MongoDB to efficiently access documents when querying MongoDB</li>
<li>The _id field is always indexed</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.tv_shows.createIndex({...})
</code></pre>
<h3 id="text-searches">Text Searches</h3>
<ul>
<li>Create a text index
<ul>
<li>However, it is only limited to 1 text index per collection</li>
</ul>
</li>
<li>Shell</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.find({
		$text: {
			$search: "word",
			$caseSensitivity : true/false
		}
	}
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	TextCriteria textCriteria <span class="token operator">=</span> TextCriteria<span class="token punctuation">.</span><span class="token function">forDefaultLanguage</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">matchingPhrase</span><span class="token punctuation">(</span><span class="token string">"fight"</span><span class="token punctuation">)</span>
	<span class="token comment">// matchingPhrase() ensures that Mongo does not treat the phrase as a bag of words</span>
	TextQuery textQuery <span class="token operator">=</span> TextQuery<span class="token punctuation">.</span><span class="token function">queryText</span><span class="token punctuation">(</span>textCriteria<span class="token punctuation">)</span>
	List<span class="token operator">&lt;</span>Document<span class="token operator">&gt;</span> results <span class="token operator">=</span> mongoTemplate<span class="token punctuation">.</span><span class="token function">find</span><span class="token punctuation">(</span>query<span class="token punctuation">,</span> Document<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> <span class="token operator">&lt;</span>collection_name<span class="token operator">&gt;</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="aggregation-1">Aggregation</h3>
<ul>
<li>Typical Pipeline
<ul>
<li>Match -&gt; Project -&gt; Group -&gt; Sort -&gt; Out</li>
</ul>
</li>
<li>Shell</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.aggregate([
		{$match : {
			&lt;column&gt;:&lt;value&gt; } 
		}
	])
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	MatchOperation matchRated <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">match</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span>
	<span class="token comment">// Place all operations inside the aggregation</span>
	Aggregation pipeline <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">newAggregation</span><span class="token punctuation">(</span>matchRated<span class="token punctuation">)</span>
	<span class="token comment">// Use .getMappedResults() on AggregationResults to get the results in List&lt;Document&gt;</span>
	AggregationResults<span class="token operator">&lt;</span>Document<span class="token operator">&gt;</span> results <span class="token operator">=</span> mongTemplate<span class="token punctuation">.</span><span class="token function">aggregate</span><span class="token punctuation">(</span>pipeline<span class="token punctuation">,</span> <span class="token operator">&lt;</span>collection_name<span class="token operator">&gt;</span><span class="token punctuation">,</span> Document<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span> 
</code></pre>
<ul>
<li>Projection</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	ProjectionOperation projectFields <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">project</span><span class="token punctuation">(</span><span class="token operator">&lt;</span>column_name<span class="token operator">&gt;</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">andExclude</span><span class="token punctuation">(</span><span class="token string">"_id"</span><span class="token punctuation">)</span>
	<span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token punctuation">)</span> is used to create a <span class="token keyword">new</span> <span class="token class-name">property</span>
	<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>column_to_add<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">as</span><span class="token punctuation">(</span>new_array_name<span class="token punctuation">)</span>
	<span class="token comment">// _id is always included by default</span>
</code></pre>
<ul>
<li>Group</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	GroupOperation groupByRated <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">group</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Sort</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	SortOperation sortByCount <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">sort</span><span class="token punctuation">(</span>Sort<span class="token punctuation">.</span><span class="token function">by</span><span class="token punctuation">(</span>Direction<span class="token punctuation">.</span>ASC<span class="token punctuation">,</span><span class="token operator">&lt;</span>column_name<span class="token operator">&gt;</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>AggregationExpression
<ul>
<li>For more complex queries, use <strong>AggregateExpression</strong> and <strong>MongoExpression</strong></li>
</ul>
</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	AggregationExpression<span class="token punctuation">.</span><span class="token function">from</span><span class="token punctuation">(</span>
		MongoExpression<span class="token punctuation">.</span><span class="token function">create</span><span class="token punctuation">(</span><span class="token string">""</span><span class="token string">" &lt;expression&gt; "</span><span class="token string">""</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Unwind
<ul>
<li>Cannot process elements in an array</li>
<li>Need to simplify the document by expanding the array</li>
<li>Final document will no longer have any array in any of its fields</li>
</ul>
</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.aggregate([
		{
			$unwind : &lt;array_name&gt;
		}
	])
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	AggregationOperation unwindGenres <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">unwind</span><span class="token punctuation">(</span><span class="token string">"genres"</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Buckets</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.movies.aggregate([
		{
			$bucket : {
				groupBy : &lt;column_name&gt;,
				boundaries: [3,5,8[
				// Create 4 boundaries, &lt;3, 3&lt;=x&lt;5, 5&lt;=x&lt;8, x &gt; 8
				default: "Others'
			}
		}
	])
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	BucketOperation bucketRating <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">bucket</span><span class="token punctuation">(</span><span class="token operator">&lt;</span>column_name<span class="token operator">&gt;</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">withBoundaries</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">withDefaultBucket</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>LookUp
<ul>
<li>Works like <strong>JOIN</strong> in MySQL</li>
<li>Comes after match operation in the aggregation pipeline</li>
</ul>
</li>
</ul>
<pre class=" language-mongo"><code class="prism  language-mongo">	db.&lt;collection_name&gt;.aggregate([
		{
			$lookup : {
				from : &lt;collection_name&gt;,
				foreignField : &lt;field_name&gt;,
				localField : &lt;field_name&gt;,
				as: "&lt;attribute_name&gt;",
				pipeline: ...
				// pipeline is a mini aggregate in a lookup used to operate on the join collectors
			}
		}
	])
</code></pre>
<ul>
<li>Java</li>
</ul>
<pre class=" language-java"><code class="prism  language-java">	LookupOperation lookupComments <span class="token operator">=</span> Aggregation<span class="token punctuation">.</span><span class="token function">lookup</span><span class="token punctuation">(</span>from<span class="token punctuation">,</span> localField<span class="token punctuation">,</span> foreignField<span class="token punctuation">,</span> as<span class="token punctuation">)</span>
</code></pre>

