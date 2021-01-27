# Cron User Stories

The following are user flows & requirements enabling cron to be utilized across many different scenarios with a simple SDK & execution flow. It is split into two sections to make the distinction between the two types of "users" within the cron system built upon NEAR.

## Contract Developers

Cron tasks will be added to any NEAR contract using a simple SDK available in Rust and AssemblyScript. Developers must define functions enabled with the SDK for cron execution to work properly.

### Schedule A new task

As a contract developer, I want to schedule a cron task to allow my code to be called one or many times in the future by paying fees up front and allowing an actor to execute my code. My contract code will give permission to the cron protocol to execute my pre-defined function using NEAR access keys. I will provide data on how to call my contract code, how often or when to call the code and any special configurations pertaining to inclusion or fee allotment. I understand that I need to pay for my tasks to execute or the scheduled task will be removed.

### Paying for future and recurring tasks

As a contract developer, I want to ensure my tasks get run at some point in the future. To ensure this happens, I allocate funds to be used to execute this task and include a little extra to pay for the protocol to trigger my task. I will provide payment to the protocol directly, paying up front for single function tasks or keeping an available balance for my account on the protocol contract. I expect to manage how my funds are allocated with a simple tool or SDK so that I don't need to understand the underlying payment system of Cron. Upon removing a recurring task, I expect to have any unused balance returned to me. I understand that all payments for task execution will be based on protocol definition and can fluctuate depending on my task configuration, market changes and protocol upgrades. Failed payments will result in cancelled task execution or task removal.

### Cancelling tasks

As a contract developer, I want to remove any task that I had previously scheduled that has a pending or future execution status. I expect a cancellation to stop all parties from calling my contract as defined in the task. I expect any already submitted and/or executed tasks to be final and un-cancelable. I expect to cancel a job by submitting a request to the Cron protocol by task ID and get a response whether the cancellation was successful or not. Cancellation timing is based on how tasks are executed within the parameters of blockchain block times and can be difficult to know an exact cancellation time; if a cancellation request is submitted within a same block range as the task pre-allocation window, Cron cannot guarantee a cancellation transaction.

### Tasks without arguments

As a contract developer, I want to configure Cron to execute a function within my code that does not require any arguments. This will allow my code to do any/all logic necessary to complete some logic utilizing local state and logic. I hope to utilize this functionality to do tasks pertaining to UX (I.E. bulk reward payouts), state management (I.E. data migrations), logical finalizations (I.E. auction or voting outcomes) or time locking (I.E. Contracts with a start or EOL date).

### Tasks with arguments

NOTE: For purposes of MVP, tasks with arguments will need further research and development. The following is the initial pass at a user story and should be considered as incomplete.

As a contract developer, I want to configure Cron tasks that contain external arguments (outside my contract state) to be provided at time of task execution to my contract code. Arguments provided to my code must match the pre-defined types as specified by the task configuration, and must be able to be verified upon and after execution. I expect the function in my code to have a baseline verification of argument data and will cover edge cases not established by the Cron protocol safety checks. External arguments can come from other contracts state, blockchain or core protocol and possibly from the outside global context of any internet enabled task runner. I expect tasks that require external arguments to incur a separate fee schedule to cover computation costs.

### Tasks timing needs

As a contract developer, I want to configure specific time parameters that match my contract outcome requirements. I expect to be able to configure a task to run only once at a future date. I expect to configure a task to run at a recurring interval over a span of time until I cancel or stop the task. I expect to be able to pay extra for a more finite window of execution. I expect to have a minimum execution time guarantee for the base task fees. Time is based on network speed and consensus between blockchain nodes, I expect to see fluctuations in exact execution time that are determined by the network and blockchain protocol. 

## Cron Task Runners

Task execution will be handled by external NEAR blockchain participant nodes that run a Cron code package. 

### Register as a task runner

As a task runner, I want to provide Cron with a reliable ongoing triggering mechanism by registering my server as an official Cron agent. I expect to create a special wallet my server can utilize to sign transactions for the NEAR blockchain. I expect to keep my server 100% accessible to the internet and to NEAR blockchain. I expect to register my server as a participant in the Cron service by submitting my server wallet account ID, account public key, reward account id and possibly a graffiti tag for friendly runner leaderboards. I expect the registration process to take some small window of block times, and potentially need to stake some NEAR tokens to help secure my place as a Cron agent. I also expect to incur fees or total stake loss upon acting maliciously toward the Cron protocol.

### Unregister as a task runner

As a task runner, I want to remove my agent from running any further cron tasks. I expect to cancel any upcoming tasks that may have been pre-assigned, but do not expect any tasks that are pending / submitted to be cancelled. For a successful unregister, I expect to withdraw any / all rewards accrued by my agent for running tasks. I expect to not be able to withdraw some or all rewards in the event my agent was deemed malicious. I expect that I can re-register at a future date if my account is deemed acceptable again in the future.

### Viewing available tasks

As a task runner, I want to view all tasks that my agent can run. I expect to be able to view this list or paginate through a list of available tasks to make sure my agent has tasks available to run. In most cases this list will be how my agent knows if it should be signing a transaction or maintaining an idle but active status.

### Executing an available task or task batch

As a task runner, I want to claim a task from the Cron queue. To claim a task, I expect my agent to autonomously request an item from Cron that I can sign as a transaction and submit to the network. Upon successful execution, I expect my agent to become available to process another task, repeating this cycle until there are no further tasks or my agent is un-registering.

### Accrueing & claiming rewards

As a task runner, I want to profit for running tasks by accruing small fees per task. My rewards will be automatically paid out directly to my configured beneficiary account ID at time of execution or in batches. To participate in being an agent, I understand that I may be required to lock an amount of NEAR within Cron as a security for upholding my agents goodwill and reputation.
