{
  "description": "Retried failed API requests up to 10 times. Adjustable retries.",
  "states": [
    {
      "name": "Trigger",
      "type": "InitialState",
      "properties": {
        "offset": {
          "x": 0,
          "y": 0
        },
        "flow_url": "https://webhooks.twilio.com/v1/Accounts/<YOUR_ACCOUNT_SID>/Flows/<YOUR_FLOW_SID>"
      },
      "transitions": [
        {
          "event": "incomingMessage",
          "conditions": [],
          "next": "FFa2e51c90655571b5ce047ca0d20e625e",
          "uuid": "4721d758-4b4f-47b8-9d72-ff5f5feec804"
        },
        {
          "event": "incomingCall",
          "conditions": [],
          "next": null,
          "uuid": "a797de9c-867b-4ddf-9deb-440b82e59429"
        },
        {
          "event": "incomingRequest",
          "conditions": [],
          "next": null,
          "uuid": "90b6a68f-e63e-4f1b-8bc5-858665fc7af1"
        }
      ],
      "sid": "FFdffc85142a3843ba64167ec661397b61"
    },
    {
      "name": "SEND_FAIL_MESSAGE",
      "type": "Message",
      "properties": {
        "offset": {
          "x": 210,
          "y": 490
        },
        "body": "Sorry, we were not able to process this request.",
        "from": "+12342184301",
        "to": "{{trigger.message.From}}",
        "media_url": null,
        "service": "{{trigger.message.InstanceSid}}",
        "channel": "{{trigger.message.ChannelSid}}",
        "attributes": null
      },
      "transitions": [
        {
          "event": "sent",
          "conditions": [],
          "next": null,
          "uuid": "5edac8f9-8108-46ce-88ca-31d217183a63"
        },
        {
          "event": "failed",
          "conditions": [],
          "next": null,
          "uuid": "26d29cbf-578f-43c0-9366-d5d861c9edb8"
        }
      ],
      "sid": "FF29f26ff647013ac4437aa2926048aeb3"
    },
    {
      "name": "SET_FAIL_COUNT",
      "type": "SetVariables",
      "properties": {
        "offset": {
          "x": -240,
          "y": 230
        },
        "variables": [
          {
            "key": "FailCount",
            "value": "{% if flow.variables.FailCount %}\n  {{flow.variables.FailCount | plus: 1}}\n{% else %}\n  1\n{% endif %}",
            "index": "0"
          }
        ]
      },
      "transitions": [
        {
          "event": "next",
          "conditions": [],
          "next": "FF4163915234d48f44126499a2074a694e",
          "uuid": "3255b7f6-ec6a-4730-a7f6-7421606e836b"
        }
      ],
      "sid": "FFa2e51c90655571b5ce047ca0d20e625e"
    },
    {
      "name": "TEST_FAIL_COUNT",
      "type": "Branch",
      "properties": {
        "offset": {
          "x": 100,
          "y": 270
        },
        "input": "{{flow.variables.FailCount}}"
      },
      "transitions": [
        {
          "event": "noMatch",
          "conditions": [],
          "next": "FFd8098899ee122019fb90cb4564bb3f55",
          "uuid": "fad9a6e3-2247-4eb8-bffc-6d19c39c5194"
        },
        {
          "event": "match",
          "conditions": [
            {
              "friendly_name": "If value equal_to 10",
              "type": "equal_to",
              "arguments": [
                "{{flow.variables.FailCount}}"
              ],
              "value": "11"
            }
          ],
          "next": "FF29f26ff647013ac4437aa2926048aeb3",
          "uuid": "76b869fd-b9ba-4c90-b10e-b770e907f9e0"
        }
      ],
      "sid": "FF4163915234d48f44126499a2074a694e"
    },
    {
      "name": "VERIFY_FUNCTION_RESPONSE",
      "type": "Branch",
      "properties": {
        "offset": {
          "x": -370,
          "y": 730
        },
        "input": "{{widgets.RUN_TIMED_RESPONSE.parsed.success}}"
      },
      "transitions": [
        {
          "event": "noMatch",
          "conditions": [],
          "next": "FFa2e51c90655571b5ce047ca0d20e625e",
          "uuid": "8df09726-c35d-4924-b27e-c06c2e1b7202"
        },
        {
          "event": "match",
          "conditions": [
            {
              "friendly_name": "RUN_TIMED_RESPONSE.parsed.success",
              "type": "is_not_blank",
              "arguments": [
                "{{widgets.RUN_TIMED_RESPONSE.parsed.success}}"
              ],
              "value": "Is Not Blank"
            }
          ],
          "next": "FF6d92d4d67bea540876759902246b47ab",
          "uuid": "63e82a15-6558-4e80-b426-c9332dd9869e"
        }
      ],
      "sid": "FFbf1877615c4d541fb7fea400c1d45a16"
    },
    {
      "name": "RUN_TIMED_RESPONSE",
      "type": "Webhook",
      "properties": {
        "offset": {
          "x": -160,
          "y": 490
        },
        "method": "GET",
        "url": "https://www.domain./path/to/your/api",
        "body": null,
        "timeout": null,
        "parameters": [
          {
            "key": "count",
            "value": "{{flow.variables.FailCount}}"
          }
        ],
        "save_response_as": null,
        "content_type": "application/x-www-form-urlencoded;charset=utf-8"
      },
      "transitions": [
        {
          "event": "success",
          "conditions": [],
          "next": "FFbf1877615c4d541fb7fea400c1d45a16",
          "uuid": "70aaf08e-0550-409a-9ceb-ebdf99952962"
        },
        {
          "event": "failed",
          "conditions": [],
          "next": "FFa2e51c90655571b5ce047ca0d20e625e",
          "uuid": "7581c35d-db90-49fb-802f-3f712470a0cc"
        }
      ],
      "sid": "FFd8098899ee122019fb90cb4564bb3f55"
    },
    {
      "name": "SEND_SUCCESS_MESSAGE",
      "type": "Message",
      "properties": {
        "offset": {
          "x": 150,
          "y": 740
        },
        "body": "Your message has been received.",
        "from": "<YOUR_TWILIO_NUMBER>",
        "to": "{{trigger.message.From}}",
        "media_url": null,
        "service": "{{trigger.message.InstanceSid}}",
        "channel": "{{trigger.message.ChannelSid}}",
        "attributes": null
      },
      "transitions": [
        {
          "event": "sent",
          "conditions": [],
          "next": null,
          "uuid": "c2347435-630d-42ad-b6e1-63008cf769d0"
        },
        {
          "event": "failed",
          "conditions": [],
          "next": null,
          "uuid": "4a9dd6b6-6e09-4c9b-939c-41b4e896f025"
        }
      ],
      "sid": "FF6d92d4d67bea540876759902246b47ab"
    }
  ]
}
