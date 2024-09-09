# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [recognize.proto](#recognize-proto)
    - [DTMFConfig](#com-cisco-wcc-ccai-v1-DTMFConfig)
    - [Duration](#com-cisco-wcc-ccai-v1-Duration)
    - [InlineGrammar](#com-cisco-wcc-ccai-v1-InlineGrammar)
    - [Model](#com-cisco-wcc-ccai-v1-Model)
    - [RecognitionFlags](#com-cisco-wcc-ccai-v1-RecognitionFlags)
    - [RecognitionRequestConfig](#com-cisco-wcc-ccai-v1-RecognitionRequestConfig)
    - [RecognitionResource](#com-cisco-wcc-ccai-v1-RecognitionResource)
    - [SpeechContext](#com-cisco-wcc-ccai-v1-SpeechContext)
    - [SpeechRecognitionAlternative](#com-cisco-wcc-ccai-v1-SpeechRecognitionAlternative)
    - [SpeechTimers](#com-cisco-wcc-ccai-v1-SpeechTimers)
    - [Status](#com-cisco-wcc-ccai-v1-Status)
    - [StreamingRecognitionResult](#com-cisco-wcc-ccai-v1-StreamingRecognitionResult)
    - [WordInfo](#com-cisco-wcc-ccai-v1-WordInfo)
  
    - [BuiltInGrammar](#com-cisco-wcc-ccai-v1-BuiltInGrammar)
    - [EnumMediaType](#com-cisco-wcc-ccai-v1-EnumMediaType)
    - [OutputEvent](#com-cisco-wcc-ccai-v1-OutputEvent)
    - [RecognitionRequestConfig.AudioEncoding](#com-cisco-wcc-ccai-v1-RecognitionRequestConfig-AudioEncoding)
    - [StreamingRecognitionResult.Role](#com-cisco-wcc-ccai-v1-StreamingRecognitionResult-Role)
  
- [Scalar Value Types](#scalar-value-types)



<a name="recognize-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## recognize.proto
This proto file has all the messages required for
STT Service and its recognize gRPC calls


<a name="com-cisco-wcc-ccai-v1-DTMFConfig"></a>

### DTMFConfig
DTMF Input Configurations


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| inter_digit_timeout | [int32](#int32) |  | Timeout between two digits |
| termchar | [string](#string) |  | Char to terminate the DTMF inputs |
| dtmf_length | [int32](#int32) |  | Max Length of DTMF to be collected |






<a name="com-cisco-wcc-ccai-v1-Duration"></a>

### Duration
Represents the Duration object denoting seconds and nanos


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| seconds | [int64](#int64) |  | Signed seconds of the span of time. Must be from -315,576,000,000 to &#43;315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min * 60 min/hr * 24 hr/day * 365.25 days/year * 10000 years |
| nanos | [int32](#int32) |  | Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to &#43;999,999,999 inclusive. |






<a name="com-cisco-wcc-ccai-v1-InlineGrammar"></a>

### InlineGrammar
InlineGrammar object with media type and grammar information


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| media_type | [EnumMediaType](#com-cisco-wcc-ccai-v1-EnumMediaType) |  | The type of media used for the inline grammar data. If not specified, let Nuance Recognizer detect the media type. |
| grammar | [string](#string) |  | Grammar data |






<a name="com-cisco-wcc-ccai-v1-Model"></a>

### Model



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| model_name | [string](#string) |  | Name of the model to be used for recognition |
| model_variant | [string](#string) |  | Variant of the model to be used for recognition |






<a name="com-cisco-wcc-ccai-v1-RecognitionFlags"></a>

### RecognitionFlags
Represents the RecognitionFlags object with boolean to enable or disable timers


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| stall_timers | [bool](#bool) |  | Whether to disable recognition timers. By default, timers start when recognition begins. |






<a name="com-cisco-wcc-ccai-v1-RecognitionRequestConfig"></a>

### RecognitionRequestConfig
Represents a recognition request config


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| encoding | [RecognitionRequestConfig.AudioEncoding](#com-cisco-wcc-ccai-v1-RecognitionRequestConfig-AudioEncoding) |  | Encoding of audio data sent in all `RecognitionAudio` messages. This field is optional for `FLAC` and `WAV` audio files and required for all other audio formats. For details, see [AudioEncoding][google.cloud.speech.v1.RecognitionConfig.AudioEncoding]. |
| sample_rate_hertz | [int32](#int32) |  | Sample rate in Hertz of the audio data sent in all `RecognitionAudio` messages. |
| language_code | [string](#string) |  | Currently, only en-US is supported. |
| max_alternatives | [int32](#int32) |  | Optional. Maximum number of recognition hypotheses to be returned. Specifically, the maximum number of `SpeechRecognitionAlternative` messages within each `SpeechRecognitionResult`. The server may return fewer than `max_alternatives`. Valid values are `0`-`30`. A value of `0` or `1` will return a maximum of one. If omitted, will return a maximum of one. |
| profanity_filter | [bool](#bool) |  | Optional. If set to `true`, the server will attempt to filter out profanities, replacing all but the initial character in each filtered word with asterisks, e.g. &#34;f***&#34;. If set to `false` or omitted, profanities won&#39;t be filtered out. Not yet supported. |
| speech_contexts | [SpeechContext](#com-cisco-wcc-ccai-v1-SpeechContext) | repeated | Optional. array of [SpeechContext][google.cloud.speech.v1.SpeechContext]. A means to provide context to assist the speech recognition. For more information, see [Phrase Hints](/speech-to-text/docs/basics#phrase-hints). |
| single_utterance | [bool](#bool) |  | Optional. If `false` or omitted, the recognizer will perform continuous recognition (continuing to wait for and process audio even if the user pauses speaking) until the client closes the input stream (gRPC API) or until the maximum time limit has been reached. May return multiple `StreamingRecognitionResult`s with the `is_final` flag set to `true`.

If `true`, the recognizer will detect a single spoken utterance. When it detects that the user has paused or stopped speaking, it will return an `END_OF_SINGLE_UTTERANCE` event and cease recognition. It will return no more than one `StreamingRecognitionResult` with the `is_final` flag set to `true`. |
| interim_results | [bool](#bool) |  | Optional If `true`, interim results (tentative hypotheses) may be returned as they become available (these interim results are indicated with the `is_final=false` flag). If `false` or omitted, only `is_final=true` result(s) are returned. |
| enable_automatic_punctuation | [bool](#bool) |  | Optional. If &#39;true&#39;, adds punctuation to recognition result hypotheses. Not yet supported. |
| speech_timers | [SpeechTimers](#com-cisco-wcc-ccai-v1-SpeechTimers) |  | Optional. Pass timer info for the recognizer |
| speech_detection_sensitivity | [float](#float) |  | A balance between detecting speech and noise (breathing, etc.), 0 to 1.0. 0 means ignore all noise, 1.0 means interpret all noise as speech. Default is 0.5. |
| nbest | [int32](#int32) |  | Maximum number of n-best hypotheses to return. Range is 0 to 999. Additional CPU cycles needed if &gt; 5. Default is 2. |
| confidence_level | [float](#float) |  | When the score of the first n-best entry is less than the value of confidencelevel, the recognition will return a no-match. Range is 0 to 1.0. Default is 0 (all utterances accepted). |
| caller_channel_number | [int32](#int32) |  | Channel number which has the caller stream in a multichannel file URL. Other streams will be considered as Agent Stream. Default value will be based on RTMS usecase |
| model | [Model](#com-cisco-wcc-ccai-v1-Model) |  | Model to be used for recognition |






<a name="com-cisco-wcc-ccai-v1-RecognitionResource"></a>

### RecognitionResource
Represents the RecognitionResource object with attributes like grammar, language and weight


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| builtInGrammar | [BuiltInGrammar](#com-cisco-wcc-ccai-v1-BuiltInGrammar) |  | Name of a builtin resource supported by the installed language pack. |
| inlineGrammar | [InlineGrammar](#com-cisco-wcc-ccai-v1-InlineGrammar) |  |  |
| language | [string](#string) |  | Mandatory. Language and country (locale) code as xx-XX (2-letters format), e.g. en-US. |
| weight | [int32](#int32) |  | Specifies the grammar&#39;s weight relative to other grammars active for that recognition. This value can range from 1 to 32767. Default is 1. |
| grammar_id | [string](#string) |  | Specifies the id that Nuance Recognizer will use to identify the grammar in the recognition result. If not set, Nuance Recognizer will generate a unique one. |






<a name="com-cisco-wcc-ccai-v1-SpeechContext"></a>

### SpeechContext
Represents a speech context message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| phrases | [string](#string) | repeated | Optional. A list of strings containing words and phrases &#34;hints&#34; so that the speech recognition is more likely to recognize them. This can be used to improve the accuracy for specific words and phrases, for example, if specific commands are typically spoken by the user. This can also be used to add additional words to the vocabulary of the recognizer. |






<a name="com-cisco-wcc-ccai-v1-SpeechRecognitionAlternative"></a>

### SpeechRecognitionAlternative
Represents the Alternative hypotheses (a.k.a. n-best list).


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| transcript | [string](#string) |  | Output only. Transcript text representing the words that the user spoke. |
| confidence | [float](#float) |  | Output only. The confidence estimate between 0.0 and 1.0. A higher number indicates an estimated greater likelihood that the recognized words are correct. This field is set only for the top alternative of a non-streaming result or, of a streaming result where `is_final=true`. Not yet supported. |
| words | [WordInfo](#com-cisco-wcc-ccai-v1-WordInfo) | repeated | Output only. A list of word-specific information for each recognized word. Note: When `enable_speaker_diarization` is true, you will see all the words from the beginning of the audio. |






<a name="com-cisco-wcc-ccai-v1-SpeechTimers"></a>

### SpeechTimers
Represents the TimerInfo object with different stats


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| no_input_timeout_ms | [int32](#int32) |  | **Deprecated.** Maximum silence, in ms, allowed while waiting for user input after recognition timers are started. A value of 0 means no timeout. |
| complete_timeout_ms | [int32](#int32) |  | Specify the duration of silence, in ms, after a valid recognition has occurred that determines the caller has finished speaking. Default is 0 (timer disabled). |
| incomplete_timeout_ms | [int32](#int32) |  | Specify the duration of silence, in ms, after an utterance before concluding that the caller has finished speaking. Default is 1500 ms. A value of 0 disables the timer. |
| max_speech_timeout_ms | [int32](#int32) |  | Maximum duration, in ms, of an utterance collected from the user. Default is 22000 ms (22 seconds). A value of -1 means no timeout. |






<a name="com-cisco-wcc-ccai-v1-Status"></a>

### Status
Represents the Status object with status code, message and description


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| code | [int32](#int32) |  | The status code, which should be an enum value of [google.rpc.Code][google.rpc.Code]. |
| message | [string](#string) |  | A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the [google.rpc.Status.details][google.rpc.Status.details] field, or localized by the client. |
| details | [string](#string) |  | Longer description if available. |






<a name="com-cisco-wcc-ccai-v1-StreamingRecognitionResult"></a>

### StreamingRecognitionResult
A streaming speech recognition result corresponding to a portion of the audio
that is currently being processed.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| alternatives | [SpeechRecognitionAlternative](#com-cisco-wcc-ccai-v1-SpeechRecognitionAlternative) | repeated | Output only. May contain one or more recognition hypotheses (up to the maximum specified in `max_alternatives`). These alternatives are ordered in terms of accuracy, with the top (first) alternative being the most probable, as ranked by the recognizer. |
| is_final | [bool](#bool) |  | Output only. If `false`, this `StreamingRecognitionResult` represents an interim result that may change. If `true`, this is the final time the speech service will return this particular `StreamingRecognitionResult`, the recognizer will not return any further hypotheses for this portion of the transcript and corresponding audio. |
| result_end_time | [Duration](#com-cisco-wcc-ccai-v1-Duration) |  | Output only. Time offset of the end of this result relative to the beginning of the audio. |
| channel_tag | [int32](#int32) |  | For multi-channel audio, this is the channel number corresponding to the recognized result for the audio from that channel. For audio_channel_count = N, its output values can range from &#39;1&#39; to &#39;N&#39;. |
| language_code | [string](#string) |  | Output only. The [BCP-47](https://www.rfc-editor.org/rfc/bcp/bcp47.txt) language tag of the language in this result. This language code was detected to have the most likelihood of being spoken in the audio. |
| has_applied_recording_offsets | [bool](#bool) |  | Whether or not recording offsets have been applied to the word alignment values. Otherwise the word alignment start and end times are only relative within the utterance. |
| speaker_ids | [uint32](#uint32) | repeated | Zero or more integers representing the speaker ID of this result. This is usually derived from the speaker integers that are passed in the streaming request. |
| last_packet_metrics_unix_timestamp_ms | [int64](#int64) |  | The unix time in milliseconds which was received from the client for the StreamingRecognizeRequest that was last used to complete this utterance. |
| message_type | [string](#string) |  | message type |
| response_event | [OutputEvent](#com-cisco-wcc-ccai-v1-OutputEvent) |  | Event Based on user utterances. |
| role | [StreamingRecognitionResult.Role](#com-cisco-wcc-ccai-v1-StreamingRecognitionResult-Role) |  |  |






<a name="com-cisco-wcc-ccai-v1-WordInfo"></a>

### WordInfo
Represents the Word-specific information for recognized words.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| start_time | [Duration](#com-cisco-wcc-ccai-v1-Duration) |  | Output only. Time offset relative to the beginning of the audio, and corresponding to the start of the spoken word. This field is only set if `enable_word_time_offsets=true` and only in the top hypothesis. This is an experimental feature and the accuracy of the time offset can vary. |
| end_time | [Duration](#com-cisco-wcc-ccai-v1-Duration) |  | Output only. Time offset relative to the beginning of the audio, and corresponding to the end of the spoken word. This field is only set if `enable_word_time_offsets=true` and only in the top hypothesis. This is an experimental feature and the accuracy of the time offset can vary. |
| word | [string](#string) |  | Output only. The word corresponding to this set of information. |





 


<a name="com-cisco-wcc-ccai-v1-BuiltInGrammar"></a>

### BuiltInGrammar
BuildInGrammar enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| Boolean | 0 |  |
| Currency | 1 |  |
| Date | 2 |  |
| Digits | 3 |  |
| Number | 4 |  |
| Phone | 5 |  |
| Time | 6 |  |
| Alphanum | 7 |  |
| Amount | 8 |  |
| Ordinal_number | 9 |  |
| Cardinal_number | 10 |  |



<a name="com-cisco-wcc-ccai-v1-EnumMediaType"></a>

### EnumMediaType
Media type enum

| Name | Number | Description |
| ---- | ------ | ----------- |
| AUTOMATIC | 0 | attempt to figure out the media type automatically. |
| APPLICATION_SRGS_XML | 1 | &#34;application/srgs&#43;xml&#34; |
| APPLICATION_X_SWI_GRAMMAR | 2 | &#34;application/x-swi-grammar&#34; |
| APPLICATION_X_SWI_PARAMETER | 3 | &#34;application/x-swi-parameter&#34; |



<a name="com-cisco-wcc-ccai-v1-OutputEvent"></a>

### OutputEvent
Return the Event based on the use input.
Similar events will be returned for Voice / DTMF based inputs.

| Name | Number | Description |
| ---- | ------ | ----------- |
| EVENT_UNSPECIFIED | 0 |  |
| EVENT_START_OF_INPUT | 1 | Triggers when user utter the first utterance in Voice Input mode or First DTMF is pressed in DTMF Input mode. This event to be used to BargeIn the prompt based on prompt barge-in flag. The event will be sent only if the current prompt being played is bargein enabled or prompt playing is complete. |
| EVENT_END_OF_INPUT | 2 | Sent when user utterance Voice / DTMF is complete. |
| EVENT_NO_MATCH | 3 | Sent when utterance did not match any of the accepted input |
| EVENT_NO_INPUT | 4 | Sent when no audio received with in the expected timeframe |



<a name="com-cisco-wcc-ccai-v1-RecognitionRequestConfig-AudioEncoding"></a>

### RecognitionRequestConfig.AudioEncoding
The encoding of the audio data sent in the request.

All encodings support only 1 channel (mono) audio.

| Name | Number | Description |
| ---- | ------ | ----------- |
| ENCODING_UNSPECIFIED | 0 | Not specified. |
| LINEAR16 | 1 | Uncompressed 16-bit signed little-endian samples (Linear PCM). |
| MULAW | 3 | 8-bit samples that compand 14-bit audio samples using G.711 PCMU/mu-law. |
| ALAW | 4 | 8-bit samples that compand 14-bit audio samples using G.711 PCMU/a-law. |



<a name="com-cisco-wcc-ccai-v1-StreamingRecognitionResult-Role"></a>

### StreamingRecognitionResult.Role


| Name | Number | Description |
| ---- | ------ | ----------- |
| UNDEFINED | 0 | Role - Undefined |
| CALLER | 1 | Role - Caller |
| AGENT | 2 | Role - Agent |


 

 

 



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

