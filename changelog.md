# API changelog

This page documents changes to the Zulip Server API over time. See
also the [Zulip release lifecycle][release-lifecycle] for background
on why this API changelog is important, and the [Zulip server
changelog][server-changelog].

The API feature levels system used in this changelog is designed to
make it possible to write API clients, such as the Zulip mobile and
terminal apps, that work with a wide range of Zulip server
versions. Every change to the Zulip API is recorded briefly here and
with full details in **Changes** entries in the API documentation for
the modified endpoint(s).

When using an API endpoint whose behavior has changed, Zulip API
clients should check the `zulip_feature_level` field, present in the
[`GET /server_settings`](/api/get-server-settings) and [`POST
/register`](/api/register-queue) responses, to determine the API
format used by the Zulip server that they are interacting with.

## Changes in Zulip 11.0

**Feature level 420**

* [`POST /mobile_push/e2ee/test_notification`](/api/e2ee-test-notify):
  Added a new endpoint to send an end-to-end encrypted test push notification
  to the user's selected mobile device or all of their mobile devices.

**Feature level 419**

* [`POST /register`](/api/register-queue): Added `simplified_presence_events`
  [client capability](/api/register-queue#parameter-client_capabilities),
  which allows clients to specify whether they support receiving the
  `presence` event type with user presence data in the modern API format.
* [`GET /events`](/api/get-events): Added the `presences` field to the
  `presence` event type for clients that support the `simplified_presence_events`
  [client capability](/api/register-queue#parameter-client_capabilities).
  The `presences` field will have the user presence data in the modern
  API format. For clients that don't support that client capability the
  event will contain fields with the legacy format for user presence data.

**Feature level 418**

* [`GET /events`](/api/get-events): An event with `type: "channel_folder"`
  and `op: "reorder"` is sent when channel folders are reordered.

**Feature level 417**

* [`POST channels/create`](/api/create-channel): Added a dedicated
  endpoint for creating a new channel. Previously, channel creation
  was done entirely through
  [`POST /users/me/subscriptions`](/api/subscribe).

**Feature level 416**

* [`POST /invites`](/api/send-invites), [`POST
  /invites/multiuse`](/api/create-invite-link): Added a new parameter
  `welcome_message_custom_text` which allows the users to add a
  Welcome Bot custom message for new users through invitations.

* [`POST /register`](/api/register-queue), [`POST /events`](/api/get-events),
  `PATCH /realm`: Added `welcome_message_custom_text` realm setting which is the
  default custom message for the Welcome Bot when sending invitations to new users.

* [`POST /realm/test_welcome_bot_custom_message`](/api/test-welcome-bot-custom-message):
  Added new endpoint test messages with the Welcome Bot custom message. The test
  messages are sent to the acting administrator, allowing them to preview how the
  custom welcome message will appear to new users upon joining the organization.