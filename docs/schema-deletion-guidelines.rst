.. _schemaregistry_deletion:

Schema Deletion Guidelines
==========================

|sr| API can delete a specific schema version or all versions of a subject. The API deletes the version but the underlying schema ID would still be available for any lookup.

.. sourcecode:: bash

    # Deletes all schema versions registered under the subject "Kafka-value"
      curl -X DELETE http://localhost:8081/subjects/Kafka-value
      [1]

    # Deletes version 1 of the schema registered under subject "Kafka-value"
      curl -X DELETE http://localhost:8081/subjects/Kafka-value/versions/1
      1

    # Deletes the most recently registered schema under subject "Kafka-value"
      curl -X DELETE http://localhost:8081/subjects/Kafka-value/versions/latest
      1

The above APIs are intended to be used be in a development environment where it's common to iterate on a schema before finalizing it. It is not recommended to use the APIs in a production environment. However, in a few scenarios these APIs can be used in production but with caution.

- A new schema to be registered has compatibility issues with one of the existing schema versions
- An old version of the schema needs to be registered again for the same subject
- The schemas are used only in real-time streaming systems and the older version(s) are absolutely no longer required
- A topic needs to be recycled

IMPORTANT! Delete Subject will delete any registered compatibility settings for the subject.  It will also delete these settings when you delete the only available schema version.
