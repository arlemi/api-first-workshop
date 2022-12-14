# API Days Paris - API First Training

This API includes supporting resources for the API First training session at API Days Paris! During the session you're going to work through generating collections from this API specification.

On completion of your submission for this training, you will receive the [Postman API First](https://badgr.com/public/badges/4ZMWYUmITU20Lf9JdAR6Xw) badge!

> 📌 Adopting a best practice approach to your API development process isn't as much of a hurdle as you might expect. By starting from an OpenAPI specification in Postman, you can generate multiple other components within a robust framework that delivers reliability and performance. Having a spec act as your single source of truth sets your API product or project up for governance, maintainability, effective adoption, and ultimately a competitive advantage.

**Before you start, make sure you have the Postman agent installed–we're going to be working in** [**Postman on the web**](http://go.postman.co/build/) **(not the desktop app). Make sure you also create a new workspace for the session–choose a Public workspace, so that you can share it later, forwarding the link to request your API First certification.** _**You will need to make your team profile public in order to publish the workspace–follow the prompts to update the info you want visitors to see.**_

## 1\. Import the starter spec

In the new workspace you created for this session (you might want to keep this tab open as well so that you can refer to the info here), choose **APIs** on the left, and click **Import**.

- Select `Link`.
- Paste `go.pstmn.io/api-first-workshop`
- **Continue**
- **Import**
    

> 📌 You can sync your Postman API with a linked spec, for example via GitHub integration.

**Open** the API–Postman will validate your schema and alert you to any issues within it. Open the `index.json` tab to see the definition JSON.

> 📌 Try introducing a syntax error into your spec file, or add an invalid element, to see how Postman highlights validation issues. Click the alert along the bottom to see more detail. As you edit, the validation will update. The editor will also prompt you with element suggestions as you type.

## 2\. The Customers specification

To get started, navigate to the API definition by opening the `index.json` file under `Definition` (you can toggle back and forth between it and the **Overview** here).

You don't need to worry too much about the detail in the spec, but note the following:

- If you check out the base URL you'll see it's initially going to hit a mock API we set up in advance, but you'll be replacing this later with your own mock.
- It includes two initial endpoints, one for retrieving a customer, and one for adding a new customer.
- The request and response body schema are defined in the `components` at the end of the spec.
- The examples include dynamic variable references (with the syntax `{{$randomValue}}`) that Postman will use to generate random property values in the docs and mocks for the collections we generate.
    

Take a quick look at the overview page in the **API** builder–we'll get to it them better as we work through the session. We'll generate collections for a few different purposes including documentation and testing, all based on the spec, and link elements such as mock servers and monitors to it so that it becomes our single source of truth for the API. Notice that you can comment and share the API to collaborate with teammates–Postman can also generate reports on your API to give stakeholders an overview of how it's performing.

## 3\. Check the documentation collection

A `Customers` collection was automatically generated when creating the API. _If you click_ _**View complete collection documentation**_ _you can see the docs straight away, or open the collection from the left and open the docs using the button to the right–_**you can keep the complete docs view open in a tab to help you work through the steps**.

> If it's easier, you can also [open the instructions on GitHub](https://github.com/arlemi/api-first-workshop/blob/main/collection-instructions.md)

Open the new collection and take a look at how the requests have been generated.
