---


---

<h1 id="csf">CSF</h1>
<h2 id="shell-commands">Shell Commands</h2>
<ul>
<li>Generate a new project</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash">ng new <span class="token operator">&lt;</span>app_name<span class="token operator">&gt;</span> --standalone<span class="token operator">=</span>false --skip-git
</code></pre>
<ul>
<li>Add additional libraries</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> <span class="token function">install</span> --save <span class="token operator">&lt;</span>module<span class="token operator">&gt;</span>
</code></pre>
<ul>
<li>Start development server</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash">ng serve
</code></pre>
<ul>
<li>Generate one or more components</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash">ng g c <span class="token operator">&lt;</span>name<span class="token operator">&gt;</span> --standalone<span class="token operator">=</span>false --skip-tests
</code></pre>
<blockquote>
<p>Don’t need to add component at the back</p>
</blockquote>
<ul>
<li>Generate service</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash">ng g s <span class="token operator">&lt;</span>service_name<span class="token operator">&gt;</span>
</code></pre>
<h2 id="accessing-properties">Accessing properties</h2>
<ul>
<li>Properties/members in the component class can be accessible by its template</li>
<li>Properties are displayed by <strong>{{ }}</strong></li>
</ul>
<h3 id="property-binding">Property Binding</h3>
<ul>
<li>Any HTML attribute can be bound to the component’s properties by surrounding the attribute name with <em>[ ]</em></li>
</ul>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>input</span> <span class="token attr-name">[value]</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>name<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
</code></pre>
<h3 id="event-binding">Event Binding</h3>
<ul>
<li>Bind HTML event with ( ) to a method/function in the component’s class
<ul>
<li>Drop the <strong>on</strong> when binding to events</li>
<li>e.g. onClick becomes (click)</li>
</ul>
</li>
<li>Pass $event into the function to get the event object</li>
<li>Communication between child and parent
<ul>
<li>@Input: Parent -&gt; child</li>
<li>@Output: Child -&gt; Parent
<ul>
<li>@Output is normally used as a Subject&lt;?&gt;</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="pipe">Pipe</h3>
<ul>
<li>Pipes are used in templates to transform values, typically for display</li>
<li>Example:</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token punctuation">{</span><span class="token punctuation">{</span> value <span class="token operator">|</span> uppercase<span class="token punctuation">}</span><span class="token punctuation">}</span>
<span class="token punctuation">{</span><span class="token punctuation">{</span> value <span class="token operator">|</span> number<span class="token punctuation">:</span><span class="token string">'1.1-3'</span> <span class="token punctuation">}</span><span class="token punctuation">}</span>
<span class="token comment">// Format decimal places</span>
<span class="token punctuation">{</span><span class="token punctuation">{</span> customer <span class="token operator">|</span> json <span class="token punctuation">}</span><span class="token punctuation">}</span>
<span class="token comment">// JSON stringify</span>
<span class="token punctuation">{</span><span class="token punctuation">{</span>name <span class="token operator">|</span> keyvalue <span class="token punctuation">}</span><span class="token punctuation">}</span>
Turn it into a map
</code></pre>
<h2 id="component-lifecycle">Component LifeCycle</h2>
<ol>
<li>ngOnInit()</li>
<li>ngOnChanges()</li>
<li>ngDoCheck()</li>
<li>ngOnDestroy()</li>
</ol>
<h2 id="forms">Forms</h2>
<h3 id="types-of-elements-in-reactiveforms">Types of elements in ReactiveForms</h3>
<ol>
<li>FormControl
<ul>
<li>Represents a form control</li>
</ul>
</li>
<li>FormGroup
<ul>
<li>Holds one or more controls, array or group</li>
</ul>
</li>
<li>FormArray
<ul>
<li>Grouping controls</li>
</ul>
</li>
</ol>
<h3 id="import-reactiveformsmodule">Import ReactiveFormsModule</h3>
<p>Add this module in app.module.ts</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">import</span> <span class="token punctuation">{</span> ReactiveFormsModule <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'@angular/forms'</span>

@<span class="token function">NgModule</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
	imports<span class="token punctuation">:</span> <span class="token punctuation">[</span>
		ReactiveFormsModule
	<span class="token punctuation">]</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="define-the-form-model">Define the Form Model</h3>
<ul>
<li>TypeScript code:</li>
</ul>
<pre class=" language-typescript"><code class="prism  language-typescript">@<span class="token function">Component</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span>
<span class="token keyword">export</span> <span class="token keyword">class</span> <span class="token class-name">RSVPComponent</span> <span class="token keyword">implements</span> <span class="token class-name">OnInit</span> <span class="token punctuation">{</span>
	rsvpForm <span class="token punctuation">:</span> FormGroup
	fb<span class="token punctuation">:</span> FormBuilder <span class="token operator">=</span> <span class="token function">inject</span><span class="token punctuation">(</span>FormBuilder<span class="token punctuation">)</span>
	
	<span class="token function">ngOnInit</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>rsvpForm <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span><span class="token function">group</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
			name<span class="token punctuation">:</span><span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span>control<span class="token operator">&lt;</span><span class="token keyword">string</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
	<span class="token punctuation">}</span>
	
</code></pre>
<ul>
<li>HTML code</li>
</ul>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>form</span> <span class="token attr-name">[formGroup]</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>rsvpForm<span class="token punctuation">"</span></span> <span class="token attr-name">(submit)</span><span class="token attr-value"><span class="token punctuation">=</span>processForm()</span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>-</span> <span class="token attr-name">formControlName</span> <span class="token attr-name">is</span> <span class="token attr-name">the</span> <span class="token attr-name">attribute</span> <span class="token attr-name">that</span> <span class="token attr-name">ties</span> <span class="token attr-name">the</span> <span class="token attr-name">input</span> <span class="token attr-name">to</span> <span class="token attr-name">the</span> <span class="token attr-name">formControl</span> <span class="token attr-name">-</span><span class="token punctuation">&gt;</span></span> 
	Name:<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>input</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>text<span class="token punctuation">"</span></span> <span class="token attr-name">formControlName</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>name<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>button</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>submit<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Send<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>button</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>form</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<ul>
<li>For FormArray:</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">export</span> <span class="token keyword">class</span> <span class="token class-name">ToDoComponent</span> <span class="token keyword">implements</span> <span class="token class-name">OnInit</span> <span class="token punctuation">{</span>
	todoForm<span class="token punctuation">:</span> FormGroup<span class="token punctuation">,</span>
	toDoArray<span class="token punctuation">:</span> FormArray
	fb<span class="token punctuation">:</span> FormBuilder <span class="token operator">=</span> <span class="token function">inject</span><span class="token punctuation">(</span>FormBuilder<span class="token punctuation">)</span>

	<span class="token function">ngOnInit</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>todoArray <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span><span class="token function">array</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>todoForm <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span><span class="token function">group</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
			todos <span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>toDoArray
		<span class="token punctuation">}</span><span class="token punctuation">)</span>
	<span class="token punctuation">}</span>

	<span class="token function">addToDo</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> 
		<span class="token keyword">const</span> toDoGroup <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span><span class="token function">group</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
			date<span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span>control<span class="token operator">&lt;</span>Date<span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
			description<span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span>control<span class="token operator">&lt;</span>string<span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
			priority<span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span>control<span class="token operator">&lt;</span>string<span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token string">''</span><span class="token punctuation">)</span>
		<span class="token punctuation">}</span><span class="token punctuation">)</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>todoArray<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>todoGroup<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
</code></pre>
<ul>
<li>HTML code:</li>
</ul>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>form</span> <span class="token attr-name">[formGroup]</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>todoForm<span class="token punctuation">"</span></span> <span class="token attr-name">(submit)</span><span class="token attr-value"><span class="token punctuation">=</span>processForm()</span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>button</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>button<span class="token punctuation">"</span></span> <span class="token attr-name">(click)</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>addToDo()<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Add TODO<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>button</span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>tbody</span> <span class="token attr-name">formArrayName</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>todos<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
		@for(todo of todoArray.controls; track $index){
			<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>tr</span> <span class="token attr-name">[formGroup]</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>todo<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
				<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>td</span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>input</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>date<span class="token punctuation">"</span></span> <span class="token attr-name">formControlName</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>date<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>td</span><span class="token punctuation">&gt;</span></span>
			<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>tr</span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>tbody</span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>button</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>submit<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>Save<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>button</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>form</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<ul>
<li>To read form values:</li>
</ul>
<pre class=" language-typescript"><code class="prism  language-typescript"><span class="token function">processForm</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token comment">//Access the value attribute to get the form values</span>
	<span class="token keyword">const</span> rsvp <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>rsvpForm<span class="token punctuation">.</span>value
<span class="token punctuation">}</span>
</code></pre>
<h3 id="validation">Validation</h3>
<ul>
<li>Set of build in validators
<ol>
<li>required</li>
<li>requiredTrue</li>
<li>email</li>
<li>min,max</li>
<li>minLength, maxLength</li>
<li>pattern</li>
</ol>
</li>
<li>To use validators:</li>
</ul>
<pre class=" language-typescript"><code class="prism  language-typescript"><span class="token keyword">import</span> <span class="token punctuation">{</span> Validators <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'@angular/forms'</span>
<span class="token function">ngOnInit</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">this</span><span class="token punctuation">.</span>rsvpForm <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span><span class="token function">group</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
		name <span class="token punctuation">:</span> <span class="token keyword">this</span><span class="token punctuation">.</span>fb<span class="token punctuation">.</span>control<span class="token operator">&lt;</span><span class="token keyword">string</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token string">''</span><span class="token punctuation">,</span><span class="token punctuation">[</span>Validators<span class="token punctuation">.</span>required<span class="token punctuation">,</span> Validators<span class="token punctuation">.</span>email<span class="token punctuation">]</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Form Validity<br>
To access, use FormGroup.valid/invalid or FormControl.valid/invalid</li>
</ul>
<pre class=" language-html"><code class="prism  language-html">&lt;input type="text" formControlName="name&gt;
@if(rsvpForm.get('name').hasError('required'){
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span><span class="token punctuation">&gt;</span></span>
		Please Enter your name
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
}
</code></pre>
<ul>
<li>Custom Validators</li>
</ul>
<blockquote>
<p>Behaviour: returns null if there is no error return a value if there is an error</p>
</blockquote>
<pre class=" language-typescript"><code class="prism  language-typescript"><span class="token keyword">import</span> <span class="token punctuation">{</span> ValidatorFn<span class="token punctuation">,</span> AbstractControl<span class="token punctuation">,</span> ValidationErrors <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'@angular/forms'</span>
<span class="token keyword">export</span> <span class="token keyword">function</span> <span class="token function">ageValidator</span><span class="token punctuation">(</span>min<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">)</span><span class="token punctuation">:</span> ValidatorFn <span class="token punctuation">{</span>
  <span class="token keyword">return</span> <span class="token punctuation">(</span>control<span class="token punctuation">:</span> AbstractControl<span class="token punctuation">)</span><span class="token punctuation">:</span> ValidationErrors <span class="token operator">|</span> <span class="token keyword">null</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>control<span class="token punctuation">.</span>value<span class="token punctuation">)</span> <span class="token keyword">return</span> <span class="token keyword">null</span><span class="token punctuation">;</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span>control<span class="token punctuation">.</span>value <span class="token operator">===</span> <span class="token string">''</span><span class="token punctuation">)</span> <span class="token keyword">return</span> <span class="token keyword">null</span><span class="token punctuation">;</span>

    <span class="token keyword">const</span> dob <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span>control<span class="token punctuation">.</span>value<span class="token punctuation">)</span><span class="token punctuation">;</span>
    console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>dob<span class="token punctuation">)</span>
    <span class="token keyword">const</span> age <span class="token operator">=</span> <span class="token function">calculateAge</span><span class="token punctuation">(</span>dob<span class="token punctuation">)</span><span class="token punctuation">;</span>
    console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>age<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span>age <span class="token operator">&gt;=</span> min<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      <span class="token keyword">return</span> <span class="token keyword">null</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
      <span class="token keyword">return</span> <span class="token punctuation">{</span> minAge<span class="token punctuation">:</span> <span class="token punctuation">{</span> min <span class="token punctuation">}</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="observables">Observables</h2>
<ul>
<li>Observables are terms that are constantly looking at the data stream</li>
<li>Example of observable operators include:
<ol>
<li>filter - filters data stream</li>
<li>map - converts a data from one type to another</li>
<li>tap - observe the data stream, used to perform side effects</li>
<li>take - take the first n value</li>
<li>switchMap - change to a different stream</li>
</ol>
</li>
</ul>
<h3 id="promise">Promise</h3>
<ul>
<li>A promise represents a pending value</li>
<li>Promises can either be
<ul>
<li>resolved - the value is ready and available
<ul>
<li>Use the then() method to follow up on what to do with the value</li>
</ul>
</li>
<li>reject - the value is not available</li>
</ul>
</li>
<li>Once a promise has been resolved, it stays resolved
<ul>
<li>Cannot reset its state, use only once</li>
</ul>
</li>
</ul>
<h3 id="httpclient">HttpClient</h3>
<ul>
<li>To use httpClient, add this in app.module.ts</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript">providers<span class="token punctuation">:</span> <span class="token punctuation">[</span>
	<span class="token function">httpClient</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token punctuation">]</span>

<span class="token comment">// Create an instance</span>
httpClient <span class="token operator">=</span> <span class="token function">inject</span><span class="token punctuation">(</span>httpClient<span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Either a promise or an observable can be used to retrieve the response from httpClient</li>
<li>Observable</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">this</span><span class="token punctuation">.</span>sub$ <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>httpClient<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token operator">&lt;</span>User<span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span><span class="token punctuation">(</span>url<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">subscribe</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
	next <span class="token punctuation">:</span> <span class="token punctuation">(</span>data<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> console<span class="token punctuation">.</span><span class="token function">info</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">,</span>
	error<span class="token punctuation">:</span> <span class="token punctuation">(</span>error<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> console<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span>error<span class="token punctuation">)</span><span class="token punctuation">,</span>
	complete<span class="token punctuation">:</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>sub$<span class="token punctuation">.</span><span class="token function">unsuscribe</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	<span class="token punctuation">}</span> 

</code></pre>
<ul>
<li>Promise</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token function">lastValueFrom</span><span class="token punctuation">(</span><span class="token keyword">this</span><span class="token punctuation">.</span>httpClient<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token operator">&lt;</span>User<span class="token operator">&gt;</span><span class="token punctuation">(</span>url<span class="token punctuation">)</span><span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span> data<span class="token punctuation">.</span>name <span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token keyword">catch</span><span class="token punctuation">(</span><span class="token punctuation">(</span>error<span class="token punctuation">:</span>HttpErrorResponse<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span> <span class="token comment">// handle error })</span>
</code></pre>
<ul>
<li>Async Pipe
<ul>
<li>Asynchronously assign the value of an observable or promist</li>
<li>If it is an observable, async pipe will automatically unsubscribe form the observable before the component is destroyed</li>
</ul>
</li>
<li>Example:</li>
</ul>
<pre class=" language-html"><code class="prism  language-html">&lt;div *ngIf="data$ | async as u; else loading&gt;
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>user-info</span> <span class="token attr-name">[user]</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>u<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>user-info</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<h3 id="http-methods">HTTP Methods</h3>
<ul>
<li>GET</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token comment">// If need params</span>
HttpParams queryParams <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HttpParams</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"custId"</span><span class="token punctuation">,</span><span class="token number">1234</span><span class="token punctuation">)</span>
<span class="token keyword">this</span><span class="token punctuation">.</span>httpClient<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> <span class="token punctuation">{</span>params <span class="token punctuation">:</span> queryParams<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>POST (JSON Payload)</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> customer<span class="token punctuation">:</span>Customer <span class="token operator">=</span> <span class="token punctuation">{</span>
	name<span class="token punctuation">:</span> <span class="token string">'barney'</span><span class="token punctuation">,</span>
	email<span class="token punctuation">:</span><span class="token string">'barney@bedrock.com'</span>
<span class="token punctuation">}</span>
<span class="token comment">// The body is the second parameter of the POST method</span>
<span class="token keyword">this</span><span class="token punctuation">.</span>httpClient<span class="token punctuation">.</span>post<span class="token operator">&lt;</span>any<span class="token operator">&gt;</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> customer<span class="token punctuation">)</span>
</code></pre>
<ul>
<li>POST (form-url encoded)</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> customer <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HttpParams</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"name"</span><span class="token punctuation">,</span><span class="token string">"barney"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"email"</span><span class="token punctuation">,</span><span class="token string">"barney@bedrock.com"</span><span class="token punctuation">)</span>

<span class="token keyword">const</span> headers <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HttpHeaders</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"Content-Type"</span><span class="token punctuation">,</span><span class="token string">"application/x-www-form-urlencoded"</span><span class="token punctuation">)</span>
<span class="token keyword">this</span><span class="token punctuation">.</span>httpClient<span class="token punctuation">.</span>post<span class="token operator">&lt;</span>any<span class="token operator">&gt;</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> customer<span class="token punctuation">.</span><span class="token function">toString</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>headers <span class="token punctuation">:</span> headers<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>
<h2 id="services">Services</h2>
<ul>
<li>Abstractions for encapsulating reusable code</li>
<li>Use cases:
<ol>
<li>Implement business logic that is independent of any components or services</li>
<li>Passing data between components or other services</li>
</ol>
</li>
<li>One way of sharing data among components: create an observable in a Service class and let components that require the data subscribe to it</li>
</ul>
<h2 id="cors">CORS</h2>
<ul>
<li>Browser will only permit certain types of cross origin resource access</li>
<li>Cross origin resource allows client to make cross origin request</li>
</ul>
<h3 id="enable-cors-in-springboot">Enable CORS in SpringBoot</h3>
<ul>
<li>Enable in SpringBoot with annotations</li>
</ul>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@RestController</span>
<span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span>path<span class="token operator">=</span><span class="token string">"/api/customer"</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@CrossOrigin</span><span class="token punctuation">(</span>origins<span class="token operator">=</span><span class="token string">"*"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">CustomerRESTController</span><span class="token punctuation">{</span>
	
	<span class="token annotation punctuation">@GetMapping</span><span class="token punctuation">(</span>path<span class="token operator">=</span><span class="token punctuation">{</span>custId<span class="token punctuation">}</span><span class="token punctuation">)</span>
	<span class="token annotation punctuation">@CrossOrigin</span><span class="token punctuation">(</span>origins<span class="token operator">=</span><span class="token string">"*"</span><span class="token punctuation">)</span>
	<span class="token keyword">public</span> ResponseEntity<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> <span class="token function">getCustomer</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> String custId<span class="token punctuation">)</span><span class="token punctuation">{</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<ul>
<li>Enable globally</li>
</ul>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">EnableCORS</span> <span class="token keyword">implements</span> <span class="token class-name">WebMvcConfigurer</span><span class="token punctuation">(</span>
	<span class="token keyword">final</span> String path<span class="token punctuation">;</span>
	<span class="token keyword">final</span> String origins<span class="token punctuation">;</span>

	<span class="token keyword">public</span> <span class="token function">EnableCORS</span><span class="token punctuation">(</span>String path<span class="token punctuation">,</span> String origins<span class="token punctuation">)</span><span class="token punctuation">{</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>path <span class="token operator">=</span> path<span class="token punctuation">;</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>origins <span class="token operator">=</span> origins<span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
	
	<span class="token annotation punctuation">@Override</span>
	<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">addCorsMapping</span><span class="token punctuation">(</span>CorsRegistry registry<span class="token punctuation">)</span><span class="token punctuation">{</span>
	registry<span class="token punctuation">.</span><span class="token function">addMapping</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">allowedOrigins</span><span class="token punctuation">(</span>origins<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>

<span class="token comment">// Initialise a bean</span>
<span class="token annotation punctuation">@Bean</span> 
<span class="token keyword">public</span> WebMvcConfigurer <span class="token function">corsConfigurer</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">EnableCORS</span><span class="token punctuation">(</span><span class="token string">"/api/*,"</span><span class="token operator">*</span>"<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token comment">// Allow all CORS on /api for all origins</span>
</code></pre>
<h2 id="routes">Routes</h2>
<ul>
<li>A route consists of:
<ol>
<li>URL</li>
<li>Component - this is the component that is loaded when the URL is activated</li>
<li>Pre-condition - for activating the route. Optional</li>
<li>Post-condition - for leaving the route. Optional.</li>
</ol>
</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> appRoutes<span class="token punctuation">:</span>Routes <span class="token operator">=</span> <span class="token punctuation">[</span>
<span class="token punctuation">{</span>path<span class="token punctuation">:</span><span class="token string">"dog"</span><span class="token punctuation">,</span>component<span class="token punctuation">:</span>DogComponent<span class="token punctuation">}</span><span class="token punctuation">,</span>
<span class="token comment">//WildCard, redirects user to a default page if path has no matches</span>
<span class="token punctuation">{</span>path<span class="token punctuation">:</span><span class="token string">"**"</span><span class="token punctuation">,</span>redirecTo<span class="token punctuation">:</span><span class="token string">"/"</span><span class="token punctuation">,</span> pathMatch<span class="token punctuation">:</span><span class="token string">"full"</span><span class="token punctuation">}</span>
<span class="token operator">...</span>
<span class="token punctuation">]</span>
</code></pre>
<h3 id="outlet">Outlet</h3>
<ul>
<li>Outlet is the location where the components for the routes to display their respective components</li>
<li> element is used to demarcate where in the app shell should the component be displayed</li>
</ul>
<h3 id="changing-client-side-route">Changing Client Side Route</h3>
<ul>
<li>A change of client’s view is triggered by changing the URL</li>
<li>Use  directive instead of href attribute in <a></a></li>
</ul>
<h3 id="changing-client-side-route-programmatically">Changing Client Side Route Programmatically</h3>
<ul>
<li>Router service exposes methods to programmatically to changes routes</li>
<li>Use navigate() method</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript">router <span class="token operator">=</span> <span class="token function">inject</span><span class="token punctuation">(</span>Router<span class="token punctuation">)</span>
<span class="token keyword">this</span><span class="token punctuation">.</span>router<span class="token punctuation">.</span><span class="token function">navigate</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token string">"/home"</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="passing-data-between-routes">Passing data between routes</h3>
<ul>
<li>Path Variable</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> appRoutes<span class="token punctuation">:</span>Routes <span class="token operator">=</span> <span class="token punctuation">[</span>
<span class="token comment">// Path variable is annotated with :{term}</span>
	<span class="token punctuation">{</span>path<span class="token punctuation">:</span><span class="token string">'customer/:custId'</span><span class="token punctuation">,</span> component<span class="token punctuation">:</span> CustomerDetailComponent<span class="token punctuation">}</span>
<span class="token punctuation">]</span>
</code></pre>
<p>-Activate parameterised route</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>!-</span> <span class="token attr-name">path</span> <span class="token attr-name">variable</span> <span class="token attr-name">is</span> <span class="token attr-name">the</span> <span class="token attr-name">second</span> <span class="token attr-name">parameter</span> <span class="token attr-name">of</span> <span class="token attr-name">routerLink</span> <span class="token attr-name">-</span><span class="token punctuation">&gt;</span></span>
&lt;a *ngFor="let c of customers"
[routerLink] = ["/customer",c.custId]&gt;
{{c.name}}
&gt;<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>a</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<ul>
<li>Query Parameters</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token comment">// Add query parameters</span>
<span class="token keyword">this</span><span class="token punctuation">.</span>router<span class="token punctuation">.</span><span class="token function">navigate</span><span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token string">'/customer'</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">{</span>queryParams <span class="token punctuation">:</span> <span class="token punctuation">{</span>view <span class="token punctuation">:</span> <span class="token string">'simple'</span><span class="token punctuation">}</span><span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Retrieving the path variables and query parameters</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript">activatedRoute <span class="token operator">=</span> <span class="token function">inject</span><span class="token punctuation">(</span>ActivatedRoute<span class="token punctuation">)</span>

<span class="token comment">// Path variable</span>
<span class="token keyword">const</span> custId <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>activatedRoute<span class="token punctuation">.</span>snapshot<span class="token punctuation">.</span>params<span class="token punctuation">.</span>custId

<span class="token comment">// Query parameters</span>
<span class="token keyword">const</span> view <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>activatedRoute<span class="token punctuation">.</span>snapshot<span class="token punctuation">.</span>queryParams<span class="token punctuation">.</span>view
</code></pre>
<h3 id="route-guards">Route Guards</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">export</span> <span class="token keyword">const</span> <span class="token function-variable function">checkIfAuthenticated</span> <span class="token operator">=</span> <span class="token punctuation">(</span>route<span class="token punctuation">:</span> ActivatedRouteSnapshot<span class="token punctuation">,</span> stateL routeStateSnapshot<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">const</span> authSvc <span class="token operator">=</span> <span class="token function">inject</span><span class="token punctuation">(</span>AuthenticationService<span class="token punctuation">)</span>
	<span class="token keyword">const</span> router <span class="token operator">=</span> <span class="token function">inject</span><span class="token punctuation">(</span>Router<span class="token punctuation">)</span>
	
	<span class="token comment">// assume a service that checks the authetication of a user</span>
	<span class="token keyword">if</span><span class="token punctuation">(</span>authSvc<span class="token punctuation">.</span><span class="token function">isAuthenticated</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
		<span class="token keyword">return</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
	<span class="token keyword">return</span> router<span class="token punctuation">.</span><span class="token function">parseUrl</span><span class="token punctuation">(</span><span class="token string">"/help"</span><span class="token punctuation">)</span>	
<span class="token punctuation">}</span>

<span class="token keyword">const</span> routes<span class="token punctuation">:</span> Routes <span class="token operator">=</span> <span class="token punctuation">[</span>
	<span class="token punctuation">{</span>path<span class="token punctuation">:</span><span class="token string">'customers'</span><span class="token punctuation">,</span> component<span class="token punctuation">:</span> CustomerListComponent<span class="token punctuation">,</span> canActivate<span class="token punctuation">:</span> <span class="token punctuation">[</span>checkIfAuthenticated<span class="token punctuation">]</span><span class="token punctuation">}</span>
<span class="token comment">// Deactivate is the same syntax, just canActivate become canDeactivate</span>
</code></pre>
<h2 id="componentstore">ComponentStore</h2>
<h3 id="storage-on-the-browser">Storage on the browser</h3>
<ul>
<li>Cookies
<ul>
<li>Used by web application to save information on the client</li>
<li>Information saved as cookies are returned to the web application whenever the browser makes a request to the server</li>
</ul>
</li>
<li>Local and Session storage
<ul>
<li>Key/value data bases</li>
<li>Values can only be strings</li>
<li>Session storage clears all data when you exit the borwser</li>
<li>Local storage will persist data across browser restarts</li>
</ul>
</li>
<li>IndexedDB
<ul>
<li>Document/object store</li>
<li>Richer data format and data type</li>
<li>Can store more data and higher performance</li>
</ul>
</li>
</ul>
<h3 id="using-localstorage">Using localStorage</h3>
<ul>
<li>It is a object in javascript, just call localStorae</li>
</ul>
<h3 id="indexeddb">IndexedDB</h3>
<ul>
<li>Has larger storage capacity than local storage</li>
<li>Can store structured data type and rich data types</li>
<li>Install with “npm install dexie”</li>
</ul>
<h3 id="create-a-database">Create a database</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">import</span> Dexie <span class="token keyword">from</span> <span class="token string">'dexie'</span>

<span class="token keyword">export</span> <span class="token keyword">class</span> <span class="token class-name">MyStore</span> <span class="token keyword">extends</span> <span class="token class-name">Dexie</span> <span class="token punctuation">{</span>
	<span class="token comment">// Table with Cart as the schema and the primary key is number</span>
	cart<span class="token punctuation">:</span>Dexie<span class="token punctuation">.</span>Table<span class="token operator">&lt;</span>Cart<span class="token punctuation">,</span> number<span class="token operator">&gt;</span>
	
	<span class="token function">constructor</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token comment">// Database name</span>
		<span class="token keyword">super</span><span class="token punctuation">(</span><span class="token string">'MyStoreDB'</span><span class="token punctuation">)</span>
		<span class="token comment">// schema version</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">version</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">stores</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
			<span class="token comment">// One or more attributes to be indexed.</span>
			cart<span class="token punctuation">:</span><span class="token string">'++cartId'</span>
		<span class="token punctuation">}</span><span class="token punctuation">)</span>
		<span class="token keyword">this</span><span class="token punctuation">.</span>cart <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">table</span><span class="token punctuation">(</span><span class="token string">'cart'</span><span class="token punctuation">)</span>

</code></pre>
<ul>
<li>version() is used to set the version of the database</li>
<li>Once created, schema cannot be changed unless the version number is increased</li>
</ul>
<h3 id="componentstore-1">ComponentStore</h3>
<ul>
<li>Add component store</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash">ng add @ngrx/component-store
</code></pre>
<ul>
<li>Store Initialisation</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> INIT_STATE<span class="token punctuation">:</span> TodoSlice <span class="token operator">=</span> <span class="token punctuation">{</span>
	todos <span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>

@<span class="token function">Injectable</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token keyword">export</span> <span class="token keyword">class</span> <span class="token class-name">TodoStore</span> <span class="token keyword">extends</span> <span class="token class-name">ComponentStore</span><span class="token operator">&lt;</span>TodoSlice<span class="token operator">&gt;</span> <span class="token punctuation">{</span>
	<span class="token function">constructor</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
		<span class="token keyword">super</span><span class="token punctuation">(</span>INIT_STATE<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<ul>
<li>Add Operation</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript">readonly addNewTodo <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>updater<span class="token operator">&lt;</span>Todo<span class="token operator">&gt;</span><span class="token punctuation">(</span>
	<span class="token comment">// Take in the slice and the item to add</span>
	<span class="token punctuation">(</span>slice<span class="token punctuation">:</span>TodoSlice<span class="token punctuation">,</span> todo<span class="token punctuation">:</span>Todo<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
		<span class="token keyword">const</span> newSlice<span class="token punctuation">:</span>TodoSlice <span class="token operator">=</span> <span class="token punctuation">{</span>
			todos<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token operator">...</span>slice<span class="token punctuation">.</span>todos<span class="token punctuation">,</span>todo<span class="token punctuation">]</span>
		<span class="token punctuation">}</span>
		<span class="token keyword">return</span> newSlice
	<span class="token punctuation">}</span>
<span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Delete operation</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript">readonly deleteTodoById <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>updater<span class="token operator">&lt;</span>string<span class="token operator">&gt;</span><span class="token punctuation">(</span>slice<span class="token punctuation">:</span> TodoSlice<span class="token punctuation">,</span> id<span class="token punctuation">:</span>string<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	todos<span class="token punctuation">:</span> slice<span class="token punctuation">.</span>todos<span class="token punctuation">.</span><span class="token function">filter</span><span class="token punctuation">(</span>todo <span class="token operator">=&gt;</span> todo<span class="token punctuation">.</span>id <span class="token operator">!==</span> id<span class="token punctuation">)</span><span class="token punctuation">}</span> <span class="token keyword">as</span> TodoSlice
	<span class="token punctuation">)</span>
<span class="token punctuation">)</span>
</code></pre>
<ul>
<li>Read Operation
<ul>
<li>select returns a function which returns an Observable</li>
</ul>
</li>
</ul>
<pre class=" language-javascript"><code class="prism  language-javascript">readonly getTodo <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span>select<span class="token operator">&lt;</span>Todo<span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">(</span>slice<span class="token punctuation">:</span>TodoSlice<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> slice<span class="token punctuation">.</span>todos<span class="token punctuation">)</span>
</code></pre>

