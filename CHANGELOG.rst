Changelog
=========

All notable changes to this project will be documented in this file.

The format is based on `Keep a Changelog`_.

  **Types of changes:**

  - **Added**: for new features.
  - **Changed**: for changes in existing functionality.
  - **Deprecated**: for soon-to-be removed features.
  - **Removed**: for now removed features.
  - **Fixed**: for any bug fixes.
  - **Security**: in case of vulnerabilities.


`UNRELEASED`_
=============

Added
-----
- Added decorator to check for C++ simulator availability (#662)
- It is possible to cancel jobs in non comercial backends (#687)
- Introduced new options for handling credentials (qiskitrc file, environment
  variables) and automatic registration. (#547)
- Add OpenMP parallelization for Apple builds of the cpp simulator (#698).

Changed
-------
- Renamed ``QISKit`` to ``Qiskit`` in the documentation. (#634)
- Use ``Qobj`` as the formally defined schema for sending information to the
  devices:
    - introduce the ``qiskit.qobj`` module. (#589, #655)
    - update the ``Qobj`` JSON schema. (#668, #677, #703, #709)
    - update the local simulators for accepting ``Qobj`` as input. (#667)
- Use ``get_status_job()`` for checking IBMQJob status. (#641)
- Q network hub/group/project credentials replaced by new url format. (#740)

Removed
-------

Fixed
-----
- Fixed ``get_ran_qasm`` methods on ``Result`` instances (#688)
- Fixed ``probabilities_ket`` computation in C++ simulator. (#580)
- Fixed bug in the definition of ``cswap`` gate and its test (#685).
- Fixed the examples to be compatible with version 0.5+ (#672)
- Fixed swap mapper using qubits after measurement (#691).
- Fixed error in cpp simulator for 3+ qubit operations (#698).
- Fixed issue with combining or extending circuits that contain CompositeGate (#710).
- Fixed the random unitary generation from the Haar measure (#760).

`0.5.6`_ - 2018-07-06
=====================

Changed
-------
- Rename repository to ``qiskit-terra`` (#606).
- Update Bloch sphere to QuTiP version (#618).
- Adjust margin of matplotlib_circuit_drawer (#632)

Removed
-------
- Remove OpenQuantumCompiler (#610).

Fixed
-----
- Fixed broken process error and simulator slowdown on Windows (#613).
- Fixed yzy_to_zyz bugs (#520, #607) by moving to quaternions (#626).


`0.5.5`_ - 2018-07-02
=====================

Added
-----
- Retrieve IBM Q jobs from server (#563, #585).
- Add German introductory documentation (``doc/de``) (#592).
- Add ``unregister()`` for removing previously registered providers (#584).
- Add matplotlib-based circuit drawer (#579).
- Adding backend filtering by least busy (#575).
- Allow running with new display names for IBMQ devices,
  and return those from ``available_backends()`` (#566)
- Introduce Qiskit Transpiler and refactor compilation flow (#578)
- Add CXCancellation pass (#578)

Changed
-------
- Remove backend filtering in individual providers, keep only in wrapper (#575).
- Single source of version information (#581)
- Bumped IBMQuantumExperience dependency to 1.9.6 (#600).
- For backend status, `status['available']` is now `status['operational']` (#609).
- Added support for registering third-party providers in `register()` (#602).
- Order strings in the output of ``available_backends()`` (#566)

Removed
-------
- Remove Clifford simulator from default available_backends, until its stable
  release (#555).
- Remove ProjectQ simulators for moving to new repository (#553).
- Remove QuantumJob class (#616)

Fixed
-----
- Fix issue with unintended inversion of initializer gates (#573).
- Fix issue with skip_transpiler causing some gates to be ignored silently (#562).


`0.5.4`_ - 2018-06-11
=====================

Added
-----

- Performance improvements:
    - remove deepcopies from dagcircuit, and extra check on qasm() (#523).

Changed
-------

- Rename repository to ``qiskit-core`` (#530).
- Repository improvements: new changelog format (#535), updated issue templates
  (#531).
- Renamed the specification schemas (#464).
- Convert ``LocalJob`` tests into unit-tests. (#526)
- Move wrapper ``load_qasm_*`` methods to a submodule (#533).

Removed
-------

- Remove Sympy simulators for moving to new repository (#514)

Fixed
-----

- Fix erroneous density matrix and probabilities in C++ simulator (#518)
- Fix hardcoded backend mapping tests (#521)
- Removed ``_modifiers call`` from ``reapply`` (#534)
- Fix circuit drawer issue with filename location on windows (#543)
- Change initial qubit layout only if the backend coupling map is not satisfied (#527)
- Fix incorrect unrolling of t to tdg in CircuitBackend (#557)
- Fix issue with simulator extension commands not reapplying correctly (#556)


`0.5.3`_ - 2018-05-29
=====================

Added
-----

- load_qasm_file / load_qasm_string methods

Changed
-------

- Dependencies version bumped

Fixed
-----

- Crash in the cpp simulator for some linux platforms
- Fixed some minor bugs


`0.5.2`_ - 2018-05-21
=====================

Changed
-------

- Adding Result.get_unitary()

Deprecated
----------

- Deprecating ``ibmqx_hpc_qasm_simulator`` and ``ibmqx_qasm_simulator`` in favor
  of ``ibmq_qasm_simulator``.

Fixed
-----

- Fixing a Mapper issue.
- Fixing Windows 7 builds.


`0.5.1`_ - 2018-05-15
=====================

- There are no code changes.

  MacOS simulator has been rebuilt with external user libraries compiled
  statically, so there’s no need for users to have a preinstalled gcc
  environment.

  Pypi forces us to bump up the version number if we want to upload a new
  package, so this is basically what have changed.


`0.5.0`_ - 2018-05-11
=====================

Improvements
------------

- Introduce providers and rework backends (#376).
    - Split backends into ``local`` and ``ibmq``.
    - Each provider derives from the following classes for its specific
      requirements (``BaseProvider``, ``BaseBackend``, ``BaseJob``).
    - Allow querying result by both circuit name and QuantumCircuit instance.
- Introduce the Qiskit ``wrapper`` (#376).
    - Introduce convenience wrapper functions around commonly used Qiskit
      components (e.g. ``compile`` and ``execute`` functions).
    - Introduce the DefaultQISKitProvider, which acts as a context manager for
      the current session (e.g. providing easy access to all
      ``available_backends``).
    - Avoid relying on QuantumProgram (eventual deprecation).
    - The functions are also available as top-level functions (for example,
      ``qiskit.get_backend()``).
- Introduce ``BaseJob`` class and asynchronous jobs (#403).
    - Return ``BaseJob`` after ``run()``.
    - Mechanisms for querying ``status`` and ``results``, or to ``cancel`` a
      job.
- Introduce a ``skip_transpiler`` flag for ``compile()`` (#411).
- Introduce schemas for validating interfaces between qiskit and backends (#434)
    - qobj_schema
    - result_schema
    - job_status_schema
    - default_pulse_config_schema
    - backend_config_schema
    - backend_props_schema
    - backend_status_schema
- Improve C++ simulator (#386)
    - Add ``tensor_index.hpp`` for multi-partite qubit vector indexing.
    - Add ``qubit_vector.hpp`` for multi-partite qubit vector algebra.
    - Rework C++ simulator backends to use QubitVector class instead of
      ``std::vector``.
- Improve interface to simulator backends (#435)
    - Introduce ``local_statevector_simulator_py`` and
      ``local_statevector_simulator_cpp``.
    - Introduce aliased and deprecated backend names and mechanisms for
      resolving them.
    - Introduce optional ``compact`` flag to query backend names only by unique
      function.
    - Introduce result convenience functions ``get_statevector``,
      ``get_unitary``
    - Add ``snapshot`` command for caching a copy of the current simulator
      state.
- Introduce circuit drawing via ``circuit_drawer()`` and
  ``plot_circuit()`` (#295, #414)
- Introduce benchmark suite for performance testing
  (``test/performance``) (#277)
- Introduce more robust probability testing via assertDictAlmostEqual (#390)
- Allow combining circuits across both depth and width (#389)
- Enforce string token names (#395)

Fixed
-----

- Fix coherent error bug in ``local_qasm_simulator_cpp`` (#318)
- Fix the order and format of result bits obtained from device backends (#430)
- Fix support for noises in the idle gate of
  ``local_clifford_simulator_cpp`` (#440)
- Fix JobProcessor modifying input qobj (#392) (and removed JobProcessor
  during #403)
- Fix ability to apply all gates on register (#369)

Deprecated
----------

- Some methods of ``QuantumProgram`` are soon to be deprecated. Please use the
  top-level functions instead.
- The ``Register`` instantiation now expects ``size, name``. Using
  ``name, size`` is still supported but will be deprecated in the future.
- Simulators no longer return wavefunction by setting shots=1. Instead,
  use the ``local_statevector_simulator``, or explicitly ask for ``snapshot``.
- Return ``job`` instance after ``run()``, rather than ``result``.
- Rename simulators according to ``PROVIDERNAME_SIMPLEALIAS_simulator_LANGUAGEORPROJECT``
- Move simulator extensions to ``qiskit/extensions/simulator``
- Move Rzz and CSwap to standard extension library


`0.4.15`_ - 2018-05-07
======================

Fixed
-----

- Fixed an issue with legacy code that was affecting Developers Challenge.


`0.4.14`_ - 2018-04-18
======================

Fixed
-----

- Fixed an issue about handling Basis Gates parameters on backend
  configurations.


`0.4.13`_ - 2018-04-16
======================

Changed
-------

- OpenQuantumCompiler.dag2json() restored for backward compatibility.

Fixed
-----

- Fixes an issue regarding barrier gate misuse in some circumstances.


`0.4.12`_ - 2018-03-11
======================

Changed
-------

- Improved circuit visualization.
- Improvements in infrastructure code, mostly tests and build system.
- Better documentation regarding contributors.

Fixed
-----

- A bunch of minor bugs have been fixed.


`0.4.11`_ - 2018-03-13
======================

Added
-----

- More testing :)

Changed
-------

- Stabilizing code related to external dependencies.

Fixed
-----

- Fixed bug in circuit drawing where some gates in the standard library
  were not plotting correctly.


`0.4.10`_ - 2018-03-06
======================

Added
-----

- Chinese translation of README.

Changed
-------

- Changes related with infrastructure (linter, tests, automation)
  enhancement.

Fixed
-----

- Fix installation issue when simulator cannot be built.
- Fix bug with auto-generated CNOT coherent error matrix in C++ simulator.
- Fix a bug in the async code.


`0.4.9`_ - 2018-02-12
=====================

Changed
-------

- CMake integration.
- QASM improvements.
- Mapper optimizer improvements.

Fixed
-----

- Some minor C++ Simulator bug-fixes.


`0.4.8`_ - 2018-01-29
=====================

Fixed
-----

- Fix parsing U_error matrix in C++ Simulator python helper class.
- Fix display of code-blocks on ``.rst`` pages.


`0.4.7`_ - 2018-01-26
=====================

Changed
-------

- Changes some naming conventions for ``amp_error`` noise parameters to
  ``calibration_error``.

Fixed
-----

- Fixes several bugs with noise implementations in the simulator.
- Fixes many spelling mistakes in simulator README.


`0.4.6`_ - 2018-01-22
=====================

Changed
-------

- We have upgraded some of out external dependencies to:

   -  matplotlib >=2.1,<2.2
   -  networkx>=1.11,<2.1
   -  numpy>=1.13,<1.15
   -  ply==3.10
   -  scipy>=0.19,<1.1
   -  Sphinx>=1.6,<1.7
   -  sympy>=1.0


`0.4.4`_ - 2018-01-09
=====================

Changed
-------

- Update dependencies to more recent versions.

Fixed
-----

- Fix bug with process tomography reversing qubit preparation order.


`0.4.3`_ - 2018-01-08
=====================

Removed
-------

- Static compilation has been removed because it seems to be failing while
  installing Qiskit via pip on Mac.


`0.4.2`_ - 2018-01-08
=====================

Fixed
-----

- Minor bug fixing related to pip installation process.


`0.4.0`_ - 2018-01-08
=====================

Added
-----

- Job handling improvements.
    - Allow asynchronous job submission.
    - New JobProcessor class: utilizes concurrent.futures.
    - New QuantumJob class: job description.
- Modularize circuit "compilation".
    Takes quantum circuit and information about backend to transform circuit
    into one which can run on the backend.
- Standardize job description.
    All backends take QuantumJob objects which wraps ``qobj`` program
    description.
- Simplify addition of backends, where circuits are run/simulated.
    - ``qiskit.backends`` package added.
    - Real devices and simulators are considered "backends" which inherent from
      ``BaseBackend``.
- Reorganize and improve Sphinx documentation.
- Improve unittest framework.
- Add tools for generating random circuits.
- New utilities for fermionic Hamiltonians (``qiskit/tools/apps/fermion``).
- New utilities for classical optimization and chemistry
  (``qiskit/tools/apps/optimization``).
- Randomized benchmarking data handling.
- Quantum tomography (``qiskit/tools/qcvv``).
    Added functions for generating, running and fitting process tomography
    experiments.
- Quantum information functions (``qiskit/tools/qi``).
    - Partial trace over subsystems of multi-partite vector.
    - Partial trace over subsystems of multi-partite matrix.
    - Flatten an operator to a vector in a specified basis.
    - Generate random unitary matrix.
    - Generate random density matrix.
    - Generate normally distributed complex matrix.
    - Generate random density matrix from Hilbert-Schmidt metric.
    - Generate random density matrix from the Bures metric.
    - Compute Shannon entropy of probability vector.
    - Compute von Neumann entropy of quantum state.
    - Compute mutual information of a bipartite state.
    - Compute the entanglement of formation of quantum state.
- Visualization improvements (``qiskit/tools``).
    - Wigner function representation.
    - Latex figure of circuit.
- Use python logging facility for info, warnings, etc.
- Auto-deployment of sphinx docs to github pages.
- Check IBMQuantumExperience version at runtime.
- Add QuantumProgram method to reconfigure already generated qobj.
- Add Japanese introductory documentation (``doc/ja``).
- Add Korean translation of readme (``doc/ko``).
- Add appveyor for continuous integration on Windows.
- Enable new IBM Q parameters for hub/group/project.
- Add QuantumProgram methods for destroying registers and circuits.
- Use Sympy for evaluating expressions.
- Add support for ibmqx_hpc_qasm_simulator backend.
- Add backend interface to Project Q C++ simulator.
    Requires installation of Project Q.
- Introduce ``InitializeGate`` class.
    Generates circuit which initializes qubits in arbitrary state.
- Introduce ``local_qiskit_simulator`` a C++ simulator with realistic noise.
    Requires C++ build environment for ``make``-based build.
- Introduce ``local_clifford_simulator`` a C++ Clifford simulator.
    Requires C++ build environment for ``make``-based build.

Changed
-------

- The standard extension for creating U base gates has been modified to be
  consistent with the rest of the gate APIs (see #203).

Removed
-------

- The ``silent`` parameter has been removed from a number of ``QuantumProgram``
  methods. The same behaviour can be achieved now by using the
  ``enable_logs()`` and ``disable_logs()`` methods, which use the standard
  Python logging.

Fixed
-----

- Fix basis gates (#76).
- Enable QASM parser to work in multiuser environments.
- Correct operator precedence when parsing expressions (#190).
- Fix "math domain error" in mapping (#111, #151).

.. _UNRELEASED: https://github.com/Qiskit/qiskit-terra/compare/0.5.6...HEAD
.. _0.5.6: https://github.com/Qiskit/qiskit-terra/compare/0.5.5...0.5.6
.. _0.5.5: https://github.com/Qiskit/qiskit-terra/compare/0.5.4...0.5.5
.. _0.5.4: https://github.com/Qiskit/qiskit-terra/compare/0.5.3...0.5.4
.. _0.5.3: https://github.com/Qiskit/qiskit-terra/compare/0.5.2...0.5.3
.. _0.5.2: https://github.com/Qiskit/qiskit-terra/compare/0.5.1...0.5.2
.. _0.5.1: https://github.com/Qiskit/qiskit-terra/compare/0.5.0...0.5.1
.. _0.5.0: https://github.com/Qiskit/qiskit-terra/compare/0.4.15...0.5.0
.. _0.4.15: https://github.com/Qiskit/qiskit-terra/compare/0.4.14...0.4.15
.. _0.4.14: https://github.com/Qiskit/qiskit-terra/compare/0.4.13...0.4.14
.. _0.4.13: https://github.com/Qiskit/qiskit-terra/compare/0.4.12...0.4.13
.. _0.4.12: https://github.com/Qiskit/qiskit-terra/compare/0.4.11...0.4.12
.. _0.4.11: https://github.com/Qiskit/qiskit-terra/compare/0.4.10...0.4.11
.. _0.4.10: https://github.com/Qiskit/qiskit-terra/compare/0.4.9...0.4.10
.. _0.4.9: https://github.com/Qiskit/qiskit-terra/compare/0.4.8...0.4.9
.. _0.4.8: https://github.com/Qiskit/qiskit-terra/compare/0.4.7...0.4.8
.. _0.4.7: https://github.com/Qiskit/qiskit-terra/compare/0.4.6...0.4.7
.. _0.4.6: https://github.com/Qiskit/qiskit-terra/compare/0.4.5...0.4.6
.. _0.4.4: https://github.com/Qiskit/qiskit-terra/compare/0.4.3...0.4.4
.. _0.4.3: https://github.com/Qiskit/qiskit-terra/compare/0.4.2...0.4.3
.. _0.4.2: https://github.com/Qiskit/qiskit-terra/compare/0.4.1...0.4.2
.. _0.4.0: https://github.com/Qiskit/qiskit-terra/compare/0.3.16...0.4.0

.. _Keep a Changelog: http://keepachangelog.com/en/1.0.0/
