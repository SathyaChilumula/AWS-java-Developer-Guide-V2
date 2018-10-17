.. Copyright 2010-2018 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

########################
Managing |EC2| Instances
########################

.. meta::
   :description: How to create, start, stop, reboot, list and monitor EC2 instances using the AWS
                 SDK for Java 2.0.
   :keywords: AWS SDK for Java 2.0, code examples, EC2 instances, create instance, start instance, stop
              instance, reboot instance, monitor instance, list instances, describe instances

.. include:: includes/dev-preview-note.txt

Creating an Instance
====================

Create a new |EC2| instance by calling the |ec2client|'s :methodname:`runInstances` method,
providing it with a :aws-java-class-prev:`RunInstancesRequest <services/ec2/model/RunInstancesRequest>`
containing the :ec2-ug:`Amazon Machine Image (AMI) <AMIs>` to use and an :ec2-ug:`instance type
<instance-types>`.

**Imports**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/CreateInstance.java
   :lines: 16-22
   :language: java

**Code**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/CreateInstance.java
   :lines: 43-76
   :dedent: 8
   :language: java

See the :sdk-examples-java-ec2:`complete example <CreateInstance.java>` on GitHub.


Starting an Instance
====================

To start an |EC2| instance, call the |ec2client|'s :methodname:`startInstances` method, providing it
with a :aws-java-class-prev:`StartInstancesRequest <services/ec2/model/StartInstancesRequest>` containing
the ID of the instance to start.

**Imports**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/StartStopInstance.java
   :lines: 16-17
   :language: java

**Code**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/StartStopInstance.java
   :lines: 27-32
   :dedent: 8
   :language: java

See the :sdk-examples-java-ec2:`complete example <StartStopInstance.java>` on GitHub.


Stopping an Instance
====================

To stop an |EC2| instance, call the |ec2client|'s :methodname:`stopInstances` method, providing it
with a :aws-java-class-prev:`StopInstancesRequest <services/ec2/model/StopInstancesRequest>` containing
the ID of the instance to stop.

**Imports**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/StartStopInstance.java
   :lines: 16, 18
   :language: java

**Code**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/StartStopInstance.java
   :lines: 39-44
   :dedent: 8
   :language: java

See the :sdk-examples-java-ec2:`complete example <StartStopInstance.java>` on GitHub.


Rebooting an Instance
=====================

To reboot an |EC2| instance, call the |ec2client|'s :methodname:`rebootInstances` method, providing it
with a :aws-java-class-prev:`RebootInstancesRequest <services/ec2/model/RebootInstancesRequest>` containing
the ID of the instance to reboot.

**Imports**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/RebootInstance.java
   :lines: 16-18
   :language: java

**Code**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/RebootInstance.java
   :lines: 38-43
   :dedent: 8
   :language: java

See the :sdk-examples-java-ec2:`complete example <RebootInstance.java>` on GitHub.


Describing Instances
====================

To list your instances, create a :aws-java-class-prev:`DescribeInstancesRequest
<services/ec2/model/DescribeInstancesRequest>` and call the |ec2client|'s
:methodname:`describeInstances` method. It will return a :aws-java-class-prev:`DescribeInstancesResponse
<services/ec2/model/DescribeInstancesResponse>` object that you can use to list the |EC2| instances
for your account and region.

Instances are grouped by *reservation*. Each reservation corresponds to the call to
:methodname:`startInstances` that launched the instance. To list your instances, you must first call
the :classname:`DescribeInstancesResponse` class' :methodname:`reservations` method, and then call
:methodname:`instances` on each returned
:aws-java-class-prev:`Reservation <services/ec2/model/Reservation>` object.

**Imports**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/DescribeInstances.java
   :lines: 16-21
   :language: java

**Code**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/DescribeInstances.java
   :lines: 32-57
   :dedent: 8
   :language: java

Results are paged; you can get further results by passing the value returned from the result
object's :methodname:`nextToken` method to a new request object's
:methodname:`nextToken` method, then using the new request object in your next call to
:methodname:`describeInstances`.

See the :sdk-examples-java-ec2:`complete example <DescribeInstances.java>` on GitHub.


Monitoring an Instance
======================

You can monitor various aspects of your |EC2| instances, such as CPU and network utilization,
available memory, and disk space remaining. To learn more about instance monitoring, see
:ec2-ug:`Monitoring Amazon EC2 <monitoring_ec2>` in the |ec2-ug|.

To start monitoring an instance, you must create a :aws-java-class-prev:`MonitorInstancesRequest
<services/ec2/model/MonitorInstancesRequest>` with the ID of the instance to monitor, and pass it to
the |ec2client|'s :methodname:`monitorInstances` method.

**Imports**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/MonitorInstance.java
   :lines: 16-17
   :language: java

**Code**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/MonitorInstance.java
   :lines: 27-32
   :dedent: 8
   :language: java

See the :sdk-examples-java-ec2:`complete example <MonitorInstance.java>` on GitHub.


Stopping Instance Monitoring
============================

To stop monitoring an instance, create an :aws-java-class-prev:`UnmonitorInstancesRequest
<services/ec2/model/UnmonitorInstancesRequest>` with the ID of the instance to stop monitoring, and
pass it to the |ec2client|'s :methodname:`unmonitorInstances` method.

**Imports**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/MonitorInstance.java
   :lines: 16, 18
   :language: java

**Code**

.. literalinclude:: example_code/ec2/src/main/java/com/example/ec2/MonitorInstance.java
   :lines: 41-46
   :dedent: 8
   :language: java

See the :sdk-examples-java-ec2:`complete example <MonitorInstance.java>` on GitHub.


More Information
================

* :ec2-api:`RunInstances` in the |ec2-api|
* :ec2-api:`DescribeInstances` in the |ec2-api|
* :ec2-api:`StartInstances` in the |ec2-api|
* :ec2-api:`StopInstances` in the |ec2-api|
* :ec2-api:`RebootInstances` in the |ec2-api|
* :ec2-api:`DescribeInstances` in the |ec2-api|
* :ec2-api:`MonitorInstances` in the |ec2-api|
* :ec2-api:`UnmonitorInstances` in the |ec2-api|
