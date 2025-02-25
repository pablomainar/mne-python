.. NOTE: we use cross-references to highlight new functions and classes.
   Please follow the examples below like :func:`mne.stats.f_mway_rm`, so the
   whats_new page will have a link to the function/class documentation.

.. NOTE: there are 3 separate sections for changes, based on type:
   - "Enhancements" for new features
   - "Bugs" for bug fixes
   - "API changes" for backward-incompatible changes

.. NOTE: changes from first-time contributors should be added to the TOP of
   the relevant section (Enhancements / Bugs / API changes), and should look
   like this (where xxxx is the pull request number):

       - description of enhancement/bugfix/API change (:gh:`xxxx` by
         :newcontrib:`Firstname Lastname`)

   Also add a corresponding entry for yourself in doc/changes/names.inc

.. _current:

Version 1.6.dev0 (development)
------------------------------

Enhancements
~~~~~~~~~~~~
- Improve tests for saving splits with :class:`mne.Epochs` (:gh:`11884` by `Dmitrii Altukhov`_)
- Added functionality for linking interactive figures together, such that changing one figure will affect another, see :ref:`tut-ui-events` and :mod:`mne.viz.ui_events`. Current figures implementing UI events are :func:`mne.viz.plot_topomap` and :func:`mne.viz.plot_source_estimates` (:gh:`11685` :gh:`11891` by `Marijn van Vliet`_)
- HTML anchors for :class:`mne.Report` now reflect the ``section-title`` of the report items rather than using a global incrementor ``global-N`` (:gh:`11890` by `Eric Larson`_)
- Added public :func:`mne.io.write_info` to complement :func:`mne.io.read_info` (:gh:`11918` by `Eric Larson`_)
- Added option ``remove_dc`` to to :meth:`Raw.compute_psd() <mne.io.Raw.compute_psd>`, :meth:`Epochs.compute_psd() <mne.Epochs.compute_psd>`, and :meth:`Evoked.compute_psd() <mne.Evoked.compute_psd>`, to allow skipping DC removal when computing Welch or multitaper spectra (:gh:`11769` by `Nikolai Chapochnikov`_)
- Add the possibility to provide a float between 0 and 1 as ``n_grad``, ``n_mag`` and ``n_eeg`` in `~mne.compute_proj_raw`, `~mne.compute_proj_epochs` and `~mne.compute_proj_evoked` to select the number of vectors based on the cumulative explained variance (:gh:`11919` by `Mathieu Scheltienne`_)
- Add extracting all time courses in a label using :func:`mne.extract_label_time_course` without applying an aggregation function (like ``mean``) (:gh:`12001` by `Hamza Abdelhedi`_)
- Added support for Artinis fNIRS data files to :func:`mne.io.read_raw_snirf` (:gh:`11926` by `Robert Luke`_)
- Add helpful error messages when using methods on empty :class:`mne.Epochs`-objects (:gh:`11306` by `Martin Schulz`_)
- Add support for passing a :class:`python:dict` as ``sensor_color`` to specify per-channel-type colors in :func:`mne.viz.plot_alignment` (:gh:`12067` by `Eric Larson`_)
- Add inferring EEGLAB files' montage unit automatically based on estimated head radius using :func:`read_raw_eeglab(..., montage_units="auto") <mne.io.read_raw_eeglab>` (:gh:`11925` by `Jack Zhang`_, :gh:`11951` by `Eric Larson`_)
- Add :class:`~mne.time_frequency.EpochsSpectrumArray` and :class:`~mne.time_frequency.SpectrumArray` to support creating power spectra from :class:`NumPy array <numpy.ndarray>` data (:gh:`11803` by `Alex Rockhill`_)
- Add support for writing forward solutions to HDF5 and convenience function :meth:`mne.Forward.save` (:gh:`12036` by `Eric Larson`_)
- Refactored internals of :func:`mne.read_annotations` (:gh:`11964` by `Paul Roujansky`_)
- Add support for drawing MEG sensors in :ref:`mne coreg` (:gh:`12098` by `Eric Larson`_)
- By default MNE-Python creates matplotlib figures with ``layout='constrained'`` rather than the default ``layout='tight'`` (:gh:`12050`, :gh:`12103` by `Mathieu Scheltienne`_ and `Eric Larson`_)
- Enhance :func:`~mne.viz.plot_evoked_field` with a GUI that has controls for time, colormap, and contour lines (:gh:`11942` by `Marijn van Vliet`_)
- Add :class:`mne.viz.ui_events.UIEvent` linking for interactive colorbars, allowing users to link figures and change the colormap and limits interactively. This supports :func:`~mne.viz.plot_evoked_topomap`, :func:`~mne.viz.plot_ica_components`, :func:`~mne.viz.plot_tfr_topomap`, :func:`~mne.viz.plot_projs_topomap`, :meth:`~mne.Evoked.plot_image`, and :meth:`~mne.Epochs.plot_image` (:gh:`12057` by `Santeri Ruuskanen`_)

Bugs
~~~~
- Fix bugs with :func:`mne.preprocessing.realign_raw` where the start of ``other`` was incorrectly cropped; and onsets and durations in ``other.annotations`` were left unsynced with the resampled data (:gh:`11950` by :newcontrib:`Qian Chu`)
- Fix bug where ``encoding`` argument was ignored when reading annotations from an EDF file (:gh:`11958` by :newcontrib:`Andrew Gilbert`)
- Mark tests ``test_adjacency_matches_ft`` and ``test_fetch_uncompressed_file`` as network tests (:gh:`12041` by :newcontrib:`Maksym Balatsko`)
- Fix bug with :func:`mne.channels.read_ch_adjacency` (:gh:`11608` by :newcontrib:`Ivan Zubarev`)
- Fix bugs with saving splits for :class:`~mne.Epochs` (:gh:`11876` by `Dmitrii Altukhov`_)
- Fix bug with multi-plot 3D rendering where only one plot was updated (:gh:`11896` by `Eric Larson`_)
- Fix bug where subject birthdays were not correctly read by :func:`mne.io.read_raw_snirf` (:gh:`11912` by `Eric Larson`_)
- Fix bug with :func:`mne.chpi.compute_head_pos` for CTF data where digitization points were modified in-place, producing an incorrect result during a save-load round-trip (:gh:`11934` by `Eric Larson`_)
- Fix bug where non-compliant stimulus data streams were not ignored by :func:`mne.io.read_raw_snirf` (:gh:`11915` by `Johann Benerradi`_)
- Fix bug with ``pca=False`` in :func:`mne.minimum_norm.compute_source_psd` (:gh:`11927` by `Alex Gramfort`_)
- Fix bug with notebooks when using PyVista 0.42 by implementing ``trame`` backend support (:gh:`11956` by `Eric Larson`_)
- Removed preload parameter from :func:`mne.io.read_raw_eyelink`, because data are always preloaded no matter what preload is set to (:gh:`11910` by `Scott Huberty`_)
- Fix bug with :meth:`mne.viz.Brain.get_view` where calling :meth:`~mne.viz.Brain.show_view` with returned parameters would change the view (:gh:`12000` by `Eric Larson`_)
- Fix bug with :meth:`mne.viz.Brain.show_view` where ``distance=None`` would change the view distance (:gh:`12000` by `Eric Larson`_)
- Fix bug with :meth:`~mne.viz.Brain.add_annotation` when reading an annotation from a file with both hemispheres shown (:gh:`11946` by `Marijn van Vliet`_)
- Fix bug with axis clip box boundaries in :func:`mne.viz.plot_evoked_topo` and related functions (:gh:`11999` by `Eric Larson`_)
- Fix bug with ``subject_info`` when loading data from and exporting to EDF file (:gh:`11952` by `Paul Roujansky`_)
- Fix rendering glitches when plotting Neuromag/TRIUX sensors in :func:`mne.viz.plot_alignment` and related functions (:gh:`12098` by `Eric Larson`_)
- Fix bug with delayed checking of :class:`info["bads"] <mne.Info>` (:gh:`12038` by `Eric Larson`_)
- Fix bug with :func:`mne.viz.plot_alignment` where ``sensor_colors`` were not handled properly on a per-channel-type basis (:gh:`12067` by `Eric Larson`_)
- Fix handling of channel information in annotations when loading data from and exporting to EDF file (:gh:`11960` :gh:`12017` :gh:`12044` by `Paul Roujansky`_)
- Add missing ``overwrite`` and ``verbose`` parameters to :meth:`Transform.save() <mne.transforms.Transform.save>` (:gh:`12004` by `Marijn van Vliet`_)
- Fix parsing of eye-link :class:`~mne.Annotations` when ``apply_offsets=False`` is provided to :func:`~mne.io.read_raw_eyelink` (:gh:`12003` by `Mathieu Scheltienne`_)
- Correctly prune channel-specific :class:`~mne.Annotations` when creating :class:`~mne.Epochs` without the channel(s) included in the channel specific annotations (:gh:`12010` by `Mathieu Scheltienne`_)
- Fix :func:`~mne.viz.plot_volume_source_estimates` with :class:`~mne.VolSourceEstimate` which include a list of vertices (:gh:`12025` by `Mathieu Scheltienne`_)
- Add support for non-ASCII characters in Annotations, Evoked comments, etc when saving to FIFF format (:gh:`12080` by `Daniel McCloy`_)
- Correctly handle passing ``"eyegaze"`` or ``"pupil"`` to :meth:`mne.io.Raw.pick` (:gh:`12019` by `Scott Huberty`_)
- Fix bug with :func:`~mne.viz.plot_raw` where changing ``MNE_BROWSER_BACKEND`` via :func:`~mne.set_config` would have no effect within a Python session (:gh:`12078` by `Santeri Ruuskanen`_)
- Improve handling of ``method`` argument in the channel interpolation function to support :class:`str` and raise helpful error messages (:gh:`12113` by `Mathieu Scheltienne`_)

API changes
~~~~~~~~~~~
- ``mne.preprocessing.apply_maxfilter`` and ``mne maxfilter`` have been deprecated and will be removed in 1.7. Use :func:`mne.preprocessing.maxwell_filter` (see :ref:`this tutorial <tut-artifact-sss>`) in Python or the command-line utility from MEGIN ``maxfilter`` and :func:`mne.bem.fit_sphere_to_headshape` instead (:gh:`11938` by `Eric Larson`_)
- :func:`mne.io.kit.read_mrk` reading pickled files is deprecated using something like ``np.savetxt(fid, pts, delimiter="\t", newline="\n")`` to save your points instead (:gh:`11937` by `Eric Larson`_)
- Replace legacy ``inst.pick_channels`` and ``inst.pick_types`` with ``inst.pick`` (where ``inst`` is an instance of :class:`~mne.io.Raw`, :class:`~mne.Epochs`, or :class:`~mne.Evoked`) wherever possible (:gh:`11907` by `Clemens Brunner`_)
- The ``reset_camera`` parameter has been removed in favor of ``distance="auto"`` in :func:`mne.viz.set_3d_view`, :meth:`mne.viz.Brain.show_view`, and related functions (:gh:`12000` by `Eric Larson`_)
