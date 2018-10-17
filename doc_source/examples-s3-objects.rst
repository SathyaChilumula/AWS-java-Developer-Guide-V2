.. Copyright 2010-2018 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

#######################################
Performing Operations on an |S3| Object
#######################################

.. meta::
    :description: How to list, upload, download or delete objects in an Amazon
                  S3 bucket using the AWS SDK for Java 2.0.
    :keywords: Amazon Simple Storage Service, Amazon S3, AWS SDK for Java 2.0 code example,
               PutObjectRequest, createMultipartUpload, GetObjectRequest

.. include:: includes/dev-preview-note.txt

An |S3| object represents a file or collection of data. Every object must be contained in a
:doc:`bucket <examples-s3-buckets>`.

.. include:: common/s3-note-incomplete-upload-policy.txt

.. include:: includes/examples-note.txt

.. contents::
    :local:
    :depth: 1


.. _upload-object:

Upload an Object
================

Build a :aws-java-class-prev:`PutObjectRequest <services/s3/model/PutObjectRequest>`
and supply a bucket name and key name. Then use the |s3client|'s
:methodname:`putObject` method with a :aws-java-class-prev:`RequestBody <core/sync/RequestBody>`
that contains the object content and the :classname:`PutObjectRequest` object.
*The bucket must exist, or the service will return an error.*

**Imports**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 22,34,38
   :language: java

**Code**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 47-51, 54-58
   :dedent: 8
   :language: java

See the :sdk-examples-java-s3:`complete example <S3ObjectOperations.java>` on GitHub.

.. _list-objects:

Upload Objects in Multiple Parts
================================

Use the |s3client|'s :methodname:`createMultipartUpload`
method to get an upload ID. Then use the :methodname:`uploadPart` method to upload each part.
Finally, use the |s3client|'s :methodname:`completeMultipartUpload` method to tell |S3| to
merge all the uploaded parts and finish the upload operation.

**Imports**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 22-25,28-29,36
   :language: java

**Code**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 151-178
   :dedent: 8
   :language: java

See the :sdk-examples-java-s3:`complete example <S3ObjectOperations.java>` on GitHub.

.. _download-object:

Download an Object
==================

Build a :aws-java-class-prev:`GetObjectRequest <services/s3/model/GetObjectRequest>`
and supply a bucket name and key name.
Use the |s3client|'s :methodname:`getObject` method, passing it the
:classname:`GetObjectRequest` object and a :classname:`ResponseTransformer` object.
The :classname:`ResponseTransformer` creates a response handler that writes
the response content to the specified file or stream.

The following example specifies a file name to write the object content to.

**Imports**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 22,32,39
   :language: java

**Code**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 110-112
   :dedent: 8
   :language: java

See the :sdk-examples-java-s3:`complete example <S3ObjectOperations.java>` on GitHub.

.. _delete-object:

Delete an Object
================

Build a :aws-java-class-prev:`DeleteObjectRequest <services/s3/model/DeleteObjectRequest>`
and supply a bucket name and key name.
Use the |s3client|'s :methodname:`deleteObject` method, and pass it the name of a bucket and
object to delete. *The specified bucket and object key must exist, or the service will return an error.*

**Imports**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 22,31
   :language: java

**Code**

.. literalinclude:: example_code/s3/src/main/java/com/example/s3/S3ObjectOperations.java
   :lines: 114-116
   :dedent: 8
   :language: java

See the :sdk-examples-java-s3:`complete example <S3ObjectOperations.java>` on GitHub.
