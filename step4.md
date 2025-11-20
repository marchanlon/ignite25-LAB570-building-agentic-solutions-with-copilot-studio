Building agentic solutions with Copilot Studio
End
Instructions
Resources
4 - Add an Agent Flow for Approving Warranty Claims
Now that we have an AI prompt that can classify warranty claims and extract key info, we're going to wrap this process in a formal, approval path based off of certain conditions like if it's in the warranty period. This is exactly what Agent Flows are for: augmenting your agents with a configurable and predictable decision path. In this section, you'll build an agent flow that reads the extracted fields, evaluates the policy conditions, and triggers an auto approval if those conditions are met.

Select Overview to get back to the overview of the agent

To create a new agent flow, scroll down to the Tools section and select Add Tool New Tool

Select New Tool in the dialog

New Tool

Select Agent Flow. This will route you to a new agent flow that you'll need to configure.

Agent Flow

You'll see two items on the screen, the trigger which kicks off the flow and the response which returns data back to the agent. The first thing we need to do is configure any inputs that we want to pass into our flow from the agent to use in the flow. To add these inputs, select the When an agent calls the flow trigger.

Flow

Select Add an input

Add Input

Select the Text option

Text Input

In the Text input type Issue Category

Issue Category

Select Add an input

Add Input

Select the Text option

Text Input

In the Text input type Purchase Date

Product Input

Select Add an input

Product Input

Select the Number option

Text Input

In the Text input type Coverage Window Days

Product Input

Select the When an agent calls the flow trigger again to collapse the inputs

Select the plus button between the when an agent calls a flow and respond to agent to add a new action.

Plus Button

Search for variable and select initialize variable

Initialize Variable

In the Name field type Approval Outcome. And in the Type dropdown select String.

Approval Outcome Variable

Select the plus button again below the initialize variable action you just added

Plus Button

Search for variable and select initialize variable

Initialize Variable

In the Name field type Approval Message. And in the Type dropdown select String.

Days Since Purchase Variable

Select the plus button again below the initialize variable action you just added

Days Since Purchase Variable

Search for variable and select initialize variable

Initialize Variable

In the Name field type Days Since Purchase. And in the Type dropdown select Integer.

Days Since Purchase Variable

In the Value Input of the Initialize Variable, select the Fx Button.

Days Since Purchase Variable

Select the Create Expression with Copilot Button

Expression with Copilot

If you don't see the Create Expression with Copilot button you can copy and paste the following formula in the formula input.

text
TypeCopy
sub(int(div(sub(ticks(utcNow()), ticks(triggerBody()?['text_4'])),864000000000)),0)
In the box type the following:

Calculate the number of days difference between the current date and the Purchase Date Input

Select Create Expression

Expression with Copilot

Verify the formula in the Suggested expression box and select the OK button.

OK Button

Verify the formula is added to the expression box and select the Add button

Add Button

Verify the expression shows in the value input as shown below, and click the arrow to close out of this panel.

Verify and Close

Click the Plus Button below the initialize variable.

Expression Filled

Search for condition and select Condition under the control header.

Select Condition

Now we need to fill out the conditions we want to check for. To do that, click in the first input and select the lightning bolt icon

Select Condition

Select the Days Since Purchase variable

Select Condition

Select the is less or equal to dropdown

Select Condition

In the right text box select the lightning bolt icon.

Select Condition

Select the Coverage Window Days Input

Select Coverage Window

Your condition should look like the screenshot below. We need to add one more condition to this.

New Condition

Select the lightning bolt icon in the left text input

Add Condition Lightning Bolt

Select the Issue Category input.

Issue Category

Change the condition dropdown to is not equal to

In the right text input type Unknown. Verify that your Condition action matches the screenshot below.

Condition Filled

Now that we have our conditions we want to check for, we need to tell the flow what would happen if it meets those conditions and what to do if it doesn't. To do this, expand out the True dropdown and select the Plus button

Yes Add

Search for variable and select the Set Variable action.

Set Variable

In the Name Dropdown select the Approval Outcome variable. In the Value input type Auto-Approved. What we're doing here is for our process, we want to auto-approve any warranty claims that aren't unknown category and are within the coverage window.

Approval Outcome Config

Now we want to fill in the approval notes. To do this, expand out the True dropdown and select the Plus button

Yes Add

Search for variable and select the Set Variable action.

Set Variable

In the Name Dropdown select the Approval Message variable. In the Value input type The Warranty Claim has been reviewed and meets all requirements to be auto-approved.

Approval Message Config

Now we need to tell the flow what to do if it doesn't meet these conditions. To configure this, expand the False section and select the Plus Button

False Condition Add

Search for variable and select the Set Variable action.

Set Variable

In the Name Dropdown select the Approval Outcome variable. In the Value input type Needs Exception Approval. This will return back to the user informing them it couldn't be auto-approved and escalation is needed

Now we want to fill in the approval notes. To do this, select the Plus button in the false condition right below the set variable you just added.

Yes Add

Search for variable and select the Set Variable action

Set Variable

In the Name Dropdown select the Approval Message variable. In the Value input type The Warranty Claim has been reviewed and it is not within the approved warranty policy guidelines. You can request a review for an exception if you'd like.

Approval Message Config

We are in the home stretch now. All that's left is to pass the data of the approval outcome back to the agent. To do that, scroll to the bottom and click to expand the Respond to the agent action and select the Add an output button

Variable Filled

Select Text for the output type

Variable Filled

Type Approval Outcome in the left text box. Click in the right text box and select the lightning bolt icon

Variable Filled

Select the Approval Outcome variable

Variable Filled

Select Add an Output again

Variable Filled

Select Text as the Output Type

Variable Filled

Type Approval Notes in the left text box. Click in the right text box and select the Lightning bolt icon.

Variable Filled

Select the Approval Message variable

Variable Filled

Select the Flow Checker button to test your flow for errors and ensure no errors are found.

Variable Filled

Select the Save Draft button

Variable Filled

Select the Overview button in the top navigation

Variable Filled

Select the Edit Button in the Details section

Variable Filled

Change the Flow Name to:

text
TypeCopy
Auto Approval Claims
In the Description input, type:

text
TypeCopy
This agent flow evaluates a warranty claim against a condition to determine if it's eligible for auto-approval or needs escalation and returns a response to the agent.
Click the Save button.

Variable Filled

Select the Designer tab in the top navigation to go back to the designer view.

Variable Filled

Select the Publish button

Variable Filled

Select the Agents tab in the left hand side to get back to your agent.

Variable Filled

Select the Zava Order Support Agent

Variable Filled

Scroll down to the Tools section and select the Add tool button

Variable Filled

Select the Flow tab

Variable Filled

Select the Auto Approval Claims flow from the list

Variable Filled

Select the Add and Configure button

Variable Filled

Select the Additional Details section and select the Agent may use this tool at any time radio button.

Variable Filled

Now we need to give additional details for how AI should pass the required inputs to the flow. To do this, scroll down to the Inputs section and select the Customize button next to the Issue Category input.

Variable Filled

In the Description text box, type

text
TypeCopy
Fill with the issue category extracted from the Claims Processing Tool
Variable Filled

Select the Customize button next to the Purchase Date input.

Variable Filled

In the Description text box, type

text
TypeCopy
Fill with the Purchase Date extracted from the Claims Processing Tool
Variable Filled

Select the Customize button next to the Coverage Window Days input.

Variable Filled

In the Description text box, type

text
TypeCopy
Fill with the numeric (in days) value of the Coverage Window extracted from the Warranty Policy
Variable Filled

Scroll down to the Completion section and select the Write the response with generative AI option from the After Running dropdown

Variable Filled

Select the Save button

Variable Filled

Select the Overview tab

Variable Filled

Select the Instructions section and select the Edit button

Variable Filled

Remove the last line about "respond in chat…". Type After all of the data is extracted, call the and put a forward slash (/) so the tool selection screen comes up and select the Auto Approval Claims tool.

Variable Filled

Finish drafting the additional instructions by pasting in the following after the tool selection:

tool. Pass all the required info and return the approval outcome for the warranty claim and approval message to the user to finish the process. Inform the user that an approval process has been started and an answer should be given shortly while you are waiting for the approval to process.

Select the Save button in the instructions section when done.

Variable Filled

You've just added an agent flow to handle warranty claim auto-approvals to your agent! Now all that's left to do is test.

1 Hr 43 Min Remaining 
