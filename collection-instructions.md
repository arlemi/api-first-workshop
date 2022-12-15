<h1 id='postman-api-days-api-first-training'>API Days Paris - API First Training</h1>
<p>You are using a collection generated from the spec for API First training session at API Days Paris!</p>
<p>So far you have imported the spec and generated a collection from it.</p>
<p>In the new collection, take a look at how the requests have been generated.</p>
<ul>
  <li>By default your requests will be grouped in folders by path (you can change this to use tags from your spec using
    the advanced settings).</li>
  <li>Your request names are pulled from the summaries in your spec.</li>
  <li>The URL indicated in the spec is stored as a collection level variable named <code>baseUrl</code>.</li>
  <li>The parameters, request bodies, and examples all populate from the examples in your spec (request details are
    auto-generated based on type if your spec doesn&#39;t include examples). <em>Since we used Postman dynamic variable
      references, the examples will regenerate each time you send a mock request or view the docs.</em></li>
</ul>
<p>Try sending the requests. <em>Initially the requests will send to the mock
    server we created before the session, but you&#39;ll send to your own mock later.</em></p>
<h2 id='1-validate'>1. Validate</h2>
<p>Postman will validate your collections against the linked spec as you work, but while you&#39;re in the request
  builder you&#39;ll only see an alert if your request is failing validation. Let&#39;s introduce an error intentionally
  so that we can see the validation in action.</p>
<ul>
  <li>In the <code>POST</code> request, edit the <strong>Body</strong> to remove the <code>id</code>, which is flagged
    as required in the spec and will therefore make the response body invalid if it isn&#39;t present.</li>
  <li><strong>Save</strong> the request–you should see a warning about the issue next to the request name. Click it to
    see further detail.</li>
  <li>Reinstate the <code>id</code> that you removed and <strong>Save</strong> the request.</li>
</ul>
<h2 id='2-view-the-docs'>2. View the docs</h2>
<p>Let&#39;s have a look at how the spec information populates into the documentation for the collection. With a request
  open, click the little docs icon at the top right.</p>
<p>Postman automatically indicates your request and response details including parameters, bodies, headers, and auth.
  You can add details by editing the information inline–edit a request description (you can use markdown) and save it.
  Click the link to view the complete docs to see how the collection as a whole is represented in docs form.</p>
<p>Check out the examples in your collection docs parameters and request / response bodies–they use the examples from
  your spec. Since we used the Postman dynamic variable syntax in the spec, your examples will dynamically generate
  random values whenever your docs are viewed. Try closing the docs tab and opening again to see this in action.</p>
<blockquote>
  <p>📌 The example name for a response comes from your API spec description for the response. If you have more than one
    response listed for a request, Postman will generate an example for each one, and your docs will present them via a
    drop-down list.</p>
</blockquote>
<p>Back to the <strong>Customers</strong>, hit <storng>Publish</storng> and publish a v1 of your API</p>
<h2 id='3-add-a-new-endpoint'>3. Add a new endpoint</h2>
<p>Let&#39;s make a change to the spec. We have endpoints for adding and retrieving a customer, but we need one for
  retrieving a list of customers.</p>
<p>In <strong>APIs</strong> &gt; <strong>Customers</strong> &gt; <strong>Definition</strong>. Add a new endpoint inside
  <code>paths</code>, after the <code>customer</code> path (adding a comma before the previous element–you can hit the
  <strong>Beautify</strong> button at the top right to clean up your indentation).</p>
<pre><code>"/customers": {
  "get": {
    "summary": "Retrieve details for all customers",
    "operationId": "listCustomers",
    "tags": [
      "customer"
    ],
    "responses": {
      "200": {
        "description": "Details of all customers",
        "content":{
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/CustomerList"
            }
          }
        }
      }
    }
  }
}</code></pre>
<p>The endpoint is going to be at the path <code>/customers</code> and will return a list of customer objects
  (referencing the existing <code>Customer</code> schema). Add the <code>CustomerList</code> schema in
  <code>components</code> &gt; <code>schemas</code> after the existing schema elements.</p>
<pre><code>"CustomerList": {
  "type": "array",
  "items": {
    "$ref": "#/components/schemas/Customer"
  }
}</code></pre>
<p><strong>Save</strong> the spec.</p>
<h2 id='4-create-a-mock-collection'>4. Create a mock collection</h2>
<p>Next we&#39;re going to create a collection we can use with a mock server we&#39;re also going to create.
<p>When we create the mock server, its address will be stored in a variable, and we will be able to switch between the
  original server and the new mock using an environment.</p>
<p><strong>Select "..."</strong> next to the collection name and <strong>Copy to Workspace</strong>. Open the <strong>Collections</strong> tab, click the <strong>"..."</strong> next to the collection name, then <strong>Mock this collection</strong>.</p>
<p>Name your mock server <code>Mock customers</code> and check the box to save the URL as an environment variable.
  Postman will create a new environment for the mock as well as generating the mock and collection.</p>
<h3 id='use-environments'>Use environments</h3>
<p>Select the new environment, it will have the same name as the mock server: <code>Mock customers</code>. Click the eye
  button to see that it has a <code>url</code> variable with the address of your new mock server–<strong>edit the
    variable name, changing it to <code>baseUrl</code></strong>.</p>
<p>Select the <code>Customer mocks</code> collection and open the collection <strong>Variables</strong>. The
  <code>baseUrl</code> includes the original URL from the spec, but by selecting the environment, the requests will
  reference the mock URL instead, because Postman scope means that the environment value overrides the collection value.
</p>
<p><strong>Send</strong> one of the requests in the mock collection. This time it will hit the new mock you created (you
  can check where it sent in the <strong>Console</strong>).</p>
<h3 id='author-examples'>Author examples</h3>
<p>You can edit your examples, for example if you prefer not to use the dynamic variables, or if you want to use a
  different one. Let&#39;s edit an example in the new mock collection to make it invalid.</p>
<ul>
  <li>Open the example for the <code>GET</code> request that retrieves a single specific customer.</li>
  <li>In the response body, remove the &quot;name&quot; property and <strong>Save</strong>.</li>
</ul>
<p><em>Make sure you reselect the mocks environment if you
    leave and return to the workspace.</em></p>
<h2 id='5-add-a-test-suite'>5. Add a test suite</h2>
<p>Combining test suites with an API-spec driven workflow builds a level of consistency and compliance into your API
  development and deployment pipeline.</p>
<p>The final collection we&#39;re going to generate is for testing. Back in the API, hit <strong>Test and Automation</strong>, click <strong>+</strong> then <strong>Generate from Defintion</strong>, with the name
  <code>Customer contract tests</code>.</p>
<p>In the new collection, open the <code>GET</code> request that returns a particular customer. In the
  <strong>Tests</strong> tab for the request, add a test from the snippets on the right (click <strong>&lt;</strong> if
  they don&#39;t display by default). Add <strong>Status code: Code is 200</strong> to the tests, <strong>Save</strong>,
  and <strong>Send</strong> the request. The test should pass.</p>
<p>Add the same snippet to the other two requests, but in the <code>POST</code> request change the code to
  <code>201</code> as follows:</p>
<pre><code>pm.test("Status code is 201", function () {
  pm.response.to.have.status(201);
});</code></pre>
<p>All of your requests should now have a test of some kind in them–to add one that looks a little more like a real
  contract test let&#39;s define a schema and validate against it in the <code>GET</code> request that retrieves a
  particular customer.</p>
<pre><code>const schema = {
 "properties": {
  "id": {
    "type": "integer"
  },
  "company": {
    "type": "string"
  },
  "name": {
    "type": "string"
  }
  }
};
pm.test("Schema is valid", function() {
 pm.response.to.have.jsonSchema(schema);
});</code></pre>
<p><strong>Save</strong> and <strong>Send</strong> the request–it should pass. Try making it fail by changing the
  <code>type</code> for <code>id</code> to <code>boolean</code>.</p>
<blockquote>
  <p>📌 Tip: leave the test failing so that you see more interesting results when you add a monitor next.</p>
</blockquote>
<p>Add a final test to the <strong>customer</strong> folder–this will run for every request inside the folder. In the
  <strong>Tests</strong> for the folder, add the following to test the response time:</p>
<pre><code>pm.test(\"Response time is less than 200ms\", function () {\n  pm.expect(pm.response.responseTime).to.be.below(200);\n});</code></pre>
<p>Try running your collection in the collection runner–go back to <strong>Test and Automation</strong> and hit <strong>Run</strong>, running with
  the default options. Check out the output, selecting requests to drill down into the detail (which you can also do in
  the <strong>Console</strong>).</p>
<h2 id='6-add-a-monitor'>6. Schedule Runs</h2>
<p>Finally, let&#39;s run the API tests on a schedule. First, copy the "Customer contract tests" collection to the workspace. Then, open it, click <strong>Run</strong>, then select
  <strong>Schedule runs</strong>.
<blockquote>
  <p>📌 A schedule run is similar to using the collection runner, or Newman/Postman CLI. It runs your collection on a schedule and alerts
    you to any failed tests by notification email.</p>
</blockquote>
<p>Give your schedule the name <code>Schedule customers tests</code>, select the <code>Mock customers</code> environment, choose
  a frequency, and create your schedule run.</p>
<p>Rather than waiting for the scheduled time, hit <strong>Run</strong>! There will be a short delay while your monitor
  runs but when it completes you will see an overview of the test results.</p>
<h2 id='7-complete-your-submission'>7. Complete your submission</h2>
<p>Once you have all of your collections generated from your spec as outlined above and you&#39;re happy with your
  workspace, you can go ahead and share it (making sure it's set to <strong>Public</strong> in the workspace overview),
  then share the link to get your API First badge!</p>
<p>When your workspace is public, anyone can open it in the browser and fork your collections to edit or send the
  requests in them. You can copy the workspace link from your browser address bar after making it public.</p>
<blockquote>
  <p>📌 Note that a Postman team admin can set the account to require approval to make a workspace public via the
    <strong>Community Manager</strong> role.</p>
</blockquote>
<p>Fill out the form <a href='https://go.pstmn.io/submit-badge'>go.pstmn.io/submit-badge</a> (if anything is missing we
  will follow up with you).</p>
