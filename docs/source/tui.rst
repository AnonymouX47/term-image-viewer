Terminal User Interface
=======================

The TUI is developed using `urwid <https://urwid.org>`_.


UI Components
-------------

| The UI consists of various areas which are each composed using one or more widgets.
| The components of the UI might change depending on the current :ref:`context <contexts>` and some :ref:`actions <actions>`.

The following are the key components that make up the UI. 

* **Banner**:

  * At the top of the UI.
  * Fixed height of 4 lines.
  * Contains the project title with a surrounding color fill and a line-box decoration.
  * Hidden in full image views.

* **Viewer**:

  * Immediately below the title banner.
  * Consists of two sub-components (described below) arranged horizontally:

    * Menu
    * View

* **Menu**:

  * Sub-component of the *viewer* to the left.
  * Fixed width of 20 columns.
  * Contains a list of image and directory entries which can be scrolled through.
  * Used to scroll through images in a directory and navigate back and forth through directories, among other actions.

* **View**:

  * Sub-component of the *viewer* to the right.
  * Images are displayed in here.
  * The content can be one of these two, depending on the type of item currently selected in the *menu*:

    * An image: When the item selected in the menu is an image.
    * An image grid: When the item selected in the menu is a directory.

  * The *view* component can also be used to scroll through images.

.. _notif-bar:

* **Notification Bar**:

  * Immediately above the *footer*.
  * Notifications about various events are displayed here.
  * Hidden in full image views.
  * Hidden in all views, in QUIET mode (:option:`-q`).

* **Footer**:

  * Displays the :ref:`actions <actions>` available in the current :ref:`context <contexts>`.
  * Each action has its name beside the symbol for the assigned key.
  * If the actions are too much to be listed on one line, the bar can be expanded/collapsed using the key indicated at the far right.

* **Overlays**:

  * These are used for various purposes such as help menu, confirmations, etc.
  * They are shown only when certain actions are triggered.

* **Info Bar**:

  * Used for debugging.
  * This is a 1-line bar immediately above the *footer*.
  * Only shows (in all views) when :option:`--debug` is specified.

Full/Maximized image views consist of only the *view* and *footer* components.


.. _contexts:

Contexts
--------

A context is simply a set of :ref:`actions <actions>`.

The active context might change due to one of these:

* Triggering certain actions.
* Change of *viewer* sub-component (i.e *menu* or *view*) in focus.
* Type of menu entry selected.
* An overlay is shown.

The active context determines which actions are available and displayed in the *footer* at the bottom of the UI.

The following are the contexts available:

* **global**: The actions in this context are available when any other context is active, with a few exceptions.

* **menu**: This context is active when the *menu* UI component is in focus and non-empty.

* **image**: This context is active if the *view* UI component is in focus and was switched to (from the *menu*) while an image entry was selected.

* **image-grid**: This context is active if the *view* UI component is in focus and was switched to (from the *menu*) while a directory entry was selected.

* **full-image**: This context is active when an image entry is maximized from the ``image`` context (using the ``Maximize`` action) or from the ``menu`` context using the ``Open`` action.

* **full-grid-image**: This context is active when an image grid cell is maximized from the ``image-grid`` context (using the ``Open`` action).

* **confirmation**: This context is active only when specific actions that require confirmation are triggered e.g the ``Delete`` action in some contexts.

* **overlay**: This context is active only when an overlay UI component (e.g the help menu) is shown.


.. _actions:

Actions
-------

An action is a single entry in a :ref:`context <contexts>`, it represents a functionality available in that context.

An action has the following defining properties:

* **name**: The name of the action.
* **key**: The key/combination used to trigger the action.
* **symbol**: A string used to represent the *key*.
* **description**: A brief description of what the action does.
* **visibility**: Determines if the action is displayed in the *footer* or not.
* **state**: Determines if the action is enabled or not.

  * If an action is disabled, pressing its *key* will trigger the terminal bell.

.. tip::

   All contexts and their actions (excluding navigation actions) with default properties
   can be found `here <https://github.com/AnonymouX47/termvisage/blob/main/default-termvisage.json>`_.
