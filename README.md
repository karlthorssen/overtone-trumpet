# overtone.inst.trumpet

Trumpet samples from freesound.org

## Usage

In project.clj,

    [overtone-trumpet "0.1.0"]

Require overtone first, as the sample loading process needs to be connected to a
supercollider server

```clojure
(require '[overtone.live :refer :all]
          [overtone.inst.trumpet :refer [sampled-trumpet]])

(sampled-trumpet) ;; plays middle c on trumpet

(sampled-trumpet :pitch 63 :attack 0.05 :level 1.5 :start-pos 0.1) ;; plays a different note
```

To control the duration of a note, use the `:gate` argument. For example,

```clojure
(defmacro play-gated [duration & body]
  `(let [duration-ms# (* 1000 ~duration)
         inst-result# ~@body]
     (at (+ (now) duration-ms#)
         (ctl inst-result# :gate 0))))

;; An A minor chord for a quarter note at 130 bpm
(doseq [midi-note [57 60 64]]
  (play-gated 0.46 (sampled-trumpet :pitch midi-note)))
```

## License

Copyright © 2019 Karl Thorssen

This program and the accompanying materials are made available under the
terms of the Eclipse Public License 2.0 which is available at
http://www.eclipse.org/legal/epl-2.0.

This Source Code may also be made available under the following Secondary
Licenses when the conditions for such availability set forth in the Eclipse
Public License, v. 2.0 are satisfied: GNU General Public License as published by
the Free Software Foundation, either version 2 of the License, or (at your
option) any later version, with the GNU Classpath Exception which is available
at https://www.gnu.org/software/classpath/license.html.
