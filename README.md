# Webots Academy Example Lesson

This repository is the demo `Visual Tracking` lesson used to show professors how to add a new lesson to Webots Academy.

![Visual Tracking Preview](assets/preview.png)

## Repository Layout

```text
.
├── README.md
├── webots.yaml
├── worlds/
│   └── visual_tracking.wbt
├── controllers/
│   ├── visual_tracker/
│   │   └── visual_tracker.py
│   └── ball_supervisor/
│       └── ball_supervisor.py
└── assets/
    ├── add_new_lesson.png
    ├── lesson_template.png
    └── preview.png
```

## What Webots Academy Reads From Your Repo

When a professor creates a lesson in Webots Academy and clicks `Sync GitHub`, the platform reads:

- `README.md` from the repo root and stores it as the lesson theory content
- `world_file` from the lesson record, which must point to the Webots `.wbt` file on GitHub
- `editable_file_path` from the lesson record, which must point to the controller file students edit
- `webots.yaml`, which Webots uses when launching the simulation environment

For this example lesson, the values are:

- `world_file`: `https://github.com/SpesRobotics/webots-academy-example/blob/main/worlds/visual_tracking.wbt`
- `editable_file_path`: `controllers/visual_tracker/visual_tracker.py`

Keep the walkthrough in this root `README.md`. Do not add a controller-local `README.md` if you want this file to remain the synced lesson content.

The screenshots in this README are referenced with relative paths from `assets/`, so they will render on GitHub after this repository is pushed.

## Step 1: Create Your Own Simulation

Create a repository that contains:

- a world file under `worlds/`
- one or more controllers under `controllers/`
- a root `README.md` that explains the lesson to students
- a `webots.yaml` file that describes how the simulation should start

You are expected to build your own simulation and your own controllers. This repository is only a reference layout.

If your lesson has support controllers such as supervisors, keep them in the repo as normal. Only the controller named by `editable_file_path` becomes the student-editable file in Webots Academy.

## Step 2: Configure `webots.yaml`

`webots.yaml` is part of the runnable lesson contract. In this example it looks like this:

```yaml
type: demo

init: |
  apt install -y \
    python3-numpy \
    python3-opencv

animation:
  worlds:
    - file: worlds/visual_tracking.wbt
      duration: 10
```

Use it to define:

- `type`: the Webots lesson mode, such as `demo`
- `init`: packages or setup commands needed before the simulation starts
- `animation.worlds`: the world file that should be launched for previews and demos

## Step 3: Push The Repo To GitHub

Webots Academy sync expects GitHub URLs. After your repo is pushed, identify:

1. the exact GitHub URL to your `.wbt` file
2. the relative path to the controller file students should edit

The URL format should look like:

```text
https://github.com/<owner>/<repo>/blob/<branch>/worlds/<lesson>.wbt
```

The editable path should look like:

```text
controllers/<controller_name>/<controller_file>.py
```

## Step 4: Create The Lesson In Webots Academy

Use the `Content Library` view and the highlighted `Create New Lesson` action:

![Create New Lesson button in Webots Academy](assets/add_new_lesson.png)

In the Webots Academy teacher dashboard:

1. Open `Content Library`
2. Click `Create New Lesson`
3. Enter the lesson title and description
4. Paste the GitHub `world_file` URL
5. Enter the `editable_file_path`
6. Save the lesson as a custom lesson

For this repository, use:

```text
world_file=https://github.com/SpesRobotics/webots-academy-example/blob/main/worlds/visual_tracking.wbt
editable_file_path=controllers/visual_tracker/visual_tracker.py
```

The lesson form should look like this when the required fields are filled:

![Lesson template fields in the Webots Academy UI](assets/lesson_template.png)

## Step 5: Sync And Preview

After the lesson is created:

1. Click `Sync GitHub`
2. Webots Academy pulls this root `README.md` into the lesson theory panel
3. Webots Academy pulls the file at `editable_file_path` into the editor starter code
4. Click `Preview` to confirm the lesson loads correctly

If you change the repo later, push the update to GitHub and click `Sync GitHub` again.

## Step 6: Assign The Lesson To Students

After the lesson is synced:

1. Create or open a class
2. Add the lesson from the class lesson manager
3. Keep the lesson visible so students can see it
4. Reorder it if needed to match your course progression

Once assigned, the lesson appears in the student dashboard like any other Webots Academy lesson.

## Official Lessons vs Custom Lessons

Professors can create and sync their own custom lessons directly from the Webots Academy UI.

Official lessons are different:

- they are seeded by Webots Academy maintainers
- they require a code change in `webots-classroom`
- they are not created by professors through the UI

For that maintainer flow, the seeded lesson metadata in `webots-classroom/backend/init_db.py` must reference the GitHub `world_file` and the `editable_file_path`.
