# ElevenLabs Music cURL Examples

Use these requests to submit a generation task and poll for the result.

## Generate

```bash
export POYO_API_KEY="YOUR_POYO_API_KEY_HERE"
export POYO_BASE_URL="https://api.poyo.ai"

curl --fail-with-body --request POST \
  --url "$POYO_BASE_URL/api/generate/submit" \
  --header "Authorization: Bearer $POYO_API_KEY" \
  --header "Content-Type: application/json" \
  --data '{
  "model": "elevenlabs-music",
  "input": {
    "text": "A clean upbeat electronic background track for a product demo video, warm synths, light percussion, modern and optimistic.",
    "duration": 30,
    "is_instrumental": true,
    "output_format": "mp3_44100_128"
  }
}'
```

Store the returned `data.task_id`, then poll:

```bash
curl --fail-with-body --request GET \
  --url "$POYO_BASE_URL/api/generate/status/task-unified-example" \
  --header "Authorization: Bearer $POYO_API_KEY"
```

## Section-Based Composition

```json
{
  "model": "elevenlabs-music",
  "input": {
    "duration": 36,
    "is_instrumental": false,
    "output_format": "mp3_44100_128",
    "composition_plan": {
      "positive_global_styles": [
        "upbeat electronic pop",
        "clean commercial production"
      ],
      "negative_global_styles": [
        "muddy mix",
        "distorted vocals"
      ],
      "sections": [
        {
          "section_name": "intro",
          "positive_local_styles": [
            "warm synth pad",
            "light percussion"
          ],
          "negative_local_styles": [
            "heavy bass"
          ],
          "duration": 12,
          "lines": [
            "A new idea starts to shine"
          ]
        },
        {
          "section_name": "hook",
          "positive_local_styles": [
            "bright chorus",
            "clear vocal melody"
          ],
          "negative_local_styles": [
            "harsh lead"
          ],
          "duration": 24,
          "lines": [
            "Build it faster, make it clear",
            "Turn the idea into something real"
          ]
        }
      ]
    }
  }
}
```

## Expected Submit Response

```json
{
  "code": 200,
  "data": {
    "task_id": "task-unified-example",
    "status": "not_started",
    "created_time": "2026-07-04T08:00:00"
  }
}
```

## Expected Status Response

```json
{
  "code": 200,
  "data": {
    "task_id": "task-unified-example",
    "status": "finished",
    "progress": 100,
    "files": [
      {
        "file_url": "https://storage.poyo.ai/generated/output-file",
        "file_type": "media"
      }
    ],
    "error_message": null
  }
}
```
