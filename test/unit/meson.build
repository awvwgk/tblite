# This file is part of tblite.
# SPDX-Identifier: LGPL-3.0-or-later
#
# tblite is free software: you can redistribute it and/or modify it under
# the terms of the GNU Lesser General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# tblite is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU Lesser General Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public License
# along with tblite.  If not, see <https://www.gnu.org/licenses/>.

# Create mstore as subproject for testing
mstore_dep = dependency(
  'mstore',
  version: '>=0.3.0',
  fallback: ['mstore', 'mstore_dep'],
  required: not meson.is_subproject(),
  default_options: [
    'default_library=static',
  ],
)
# If we do not find mstore and are a subproject, we just skip testing
if not mstore_dep.found()
  subdir_done()
endif

tests = [
  'cgto-ortho',
  'coulomb-charge',
  'coulomb-multipole',
  'coulomb-thirdorder',
  'double-dictionary',
  'fit',
  'gfn1-xtb',
  'gfn2-xtb',
  'ceh',
  'hamiltonian',
  'halogen',
  'integral-overlap',
  'integral-multipole',
  'ipea1-xtb',
  'ncoord',
  'npy',
  'npz',
  'post-processing',
  'repulsion',
  'slater-expansion',
  'spin',
  'solvation-born',
  'solvation-cpcm',
  'solvation-surface',
  'solvation-cds',
  'solvation-shift',
  'tagged-io',
  'wavefunction-restart',
  'xtb-param',
  'xtb-external',
  'xtbml',
]

test_srcs = files(
  'main.f90',
)
foreach t : tests
  test_srcs += files('test_@0@.f90'.format(t.underscorify()))
endforeach

tester = executable(
  'tester',
  sources: test_srcs,
  dependencies: [tblite_dep, mstore_dep],
  link_language: 'fortran',
)

foreach t : tests
  test(t, tester, args: t, suite: 'unit')
endforeach
