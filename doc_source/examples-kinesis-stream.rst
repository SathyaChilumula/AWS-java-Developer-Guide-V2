.. Copyright 2010-2018 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

##########################################
Subscribing to Amazon Kinesis Data Streams
##########################################

.. meta::
    :description: How to use Amazon Kinesis data streams to get results from Amazon Kinesis using the AWS SDK for Java 2.0.
    :keywords: Kinesis, AWS SDK for Java 2.0, async streaming

The following examples show you how to retrieve and process data from |AKSlong|
using the :methodname:`subscribeToShard` method.
|AKS| now employs the enhanced fanout feature and a
low-latency HTTP/2 data retrieval API, making it
easier for developers to run multiple low-latency, high-performance applications
on the same |AK| Data Stream.


Set Up
======

First, create an asynchronous |AK| client and a
:aws-java-class:`SubscribeToShardRequest <services/kinesis/model/SubscribeToShardRequest>` object.
These objects are used in each of the following examples to subscribe to |AK| events.

**Imports**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
   :lines: 17-37
   :language: java

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
   :lines: 227-233
   :dedent: 8
   :language: java


Use the Builder Interface
=========================

You can use the :methodname:`builder` method to simplify the creation of the
:aws-java-class:`SubscribeToShardResponseHandler <services/kinesis/model/SubscribeToShardResponseHandler>`.

Using the builder, you can set each lifecycle callback with a method call instead of implementing
the full interface.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
  :lines: 45-54
  :dedent: 4
  :language: java

For more control of the publisher, you can use the :methodname:`publisherTransformer`
method to customize the publisher.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
  :lines: 71-79
  :dedent: 4
  :language: java

See the :sdk-examples-java-kinesis:`complete example <KinesisStreamEx.java>` on GitHub.

Use a Custom Response Handler
=============================

For full control of the subscriber and publisher, implement the
:aws-java-class:`SubscribeToShardResponseHandler <services/kinesis/model/SubscribeToShardResponseHandler>` interface.

In this example, you implement the :methodname:`onEventStream` method, which allows
you full access to the publisher. This demonstrates how to transform the publisher to
event records for printing by the subscriber.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
   :lines: 119-154
   :dedent: 4
   :language: java

See the :sdk-examples-java-kinesis:`complete example <KinesisStreamEx.java>` on GitHub.

Use the Visitor Interface
=========================

You can use a
:aws-java-class:`Visitor <services/kinesis/model/SubscribeToShardResponseHandler\Visitor>` object
to subscribe to specific events you're interested in watching.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
   :lines: 85-96
   :dedent: 4
   :language: java

See the :sdk-examples-java-kinesis:`complete example <KinesisStreamEx.java>` on GitHub.

Use a Custom Subscriber
=======================

You can also implement your own custom subscriber to subscribe to the stream.

This code snippet shows an example subscriber.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
   :lines: 184-214
   :dedent: 4
   :language: java

You can pass that custom subscriber to the :methodname:`subscribe` method, similarly
to preview examples. The following code snippet shows this example.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamEx.java
   :lines: 159-166
   :dedent: 4
   :language: java

See the :sdk-examples-java-kinesis:`complete example <KinesisStreamEx.java>` on GitHub.

Use a Third-Party Library
==========================

You can use other third-party libraries instead of implementing a custom subscriber.
This example demonstrates using the RxJava implementation,
but you can use any library that implements the Reactive Streams interfaces.
See the `RxJava wiki page on Github <https://github.com/ReactiveX/RxJava/wiki>`_
for more information on that library.

To use the library, add it as a dependency. If you're using Maven, the example shows the
POM snippet to use.

**POM Entry**

.. literalinclude:: example_code/kinesis/pom.xml
   :lines: 13-17
   :language: xml

**Imports**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamRxJavaEx.java
  :lines: 17-33
  :language: java

This example uses RxJava in the :methodname:`onEventStream` lifecycle method. This gives you
full access to the publisher, which can be used to create an Rx Flowable.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamRxJavaEx.java
  :lines: 45-54
  :dedent: 8
  :language: java

You can also use the :methodname:`publisherTransformer` method with the :methodname:`Flowable`
publisher. You must adapt the :methodname:`Flowable` publisher to an `SdkPublisher`, as shown in
the following example.

**Code**

.. literalinclude:: example_code/kinesis/src/main/java/com/example/kinesis/KinesisStreamRxJavaEx.java
  :lines: 64-68
  :dedent: 8
  :language: java

See the :sdk-examples-java-kinesis:`complete example <KinesisStreamRxJavaEx.java>` on GitHub.

More Information
================

* :AK-api:`SubscribeToShardEvent <API_SubscribeToShardEvent>` in the |AK-api|
* :AK-api:`SubscribeToShard <API_SubscribeToShard>` in the |AK-api|
