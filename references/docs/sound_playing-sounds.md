 about

Playing Sounds

s&box provides several ways to play sounds in code. You can fire-and-forget a sound at a world position,

control it via a SoundHandle , attach it to a GameObject , or use scene components entirely.

SoundEvent

Most sounds in s&box are defined as SoundEvent assets ( .sound files). A SoundEvent bundles one or

more audio files together with settings like volume range, pitch range, 3D distance, occlusion, and a

selection mode (random, sequential, etc.).

Reference a SoundEvent from a property on your component:

[Property] public SoundEvent FootstepSound { get; set; }

You can also load one by path at runtime:

var sound = ResourceLibrary.Get<SoundEvent>( "sounds/footsteps/concrete.sound" );

The UI flag on a SoundEvent makes it play as a flat 2D sound with no distance attenuation -

useful for interface and HUD audio.

Sound.Play

Sound.Play is the primary static API for playing sounds in code. It returns a SoundHandle you can use to

control the sound later.

Basic playback

// By SoundEvent reference
Sound.Play( FootstepSound );

// By asset path (string)
Sound.Play( "sounds/explosion.sound" );

// By asset name (string), can be placed in any folder but must be unique
Sound.Play( "explosion_large" );

3D posit ional sound

Pass a world-space Vector3 to place the sound in the scene:

Sound.Play( ExplosionSound, WorldPosition );
Sound.Play( "sounds/explosion.sound", transform.Position );

Without a position the sound defaults to the world origin (0, 0, 0) . For a sound that should follow an

object, use GameObject.PlaySound instead (see below).

Fade in

An optional fadeInTime parameter fades the volume up from silence over the given number of seconds:

Sound.Play( AmbientSound, WorldPosition, fadeInTime: 2.0f );

SoundHandle

Every Sound.Play call returns a SoundHandle . Keep a reference to it when you need to change or stop the

sound after it starts.

SoundHandle _engineLoop;

void StartEngine()
 _engineLoop = Sound.Play( EngineLoopSound, WorldPosition );
 _engineLoop.Volume = 0.8f;
 _engineLoop.Pitch = 1.2f;

Key propert ies

P r o p e r t y

D e s c r ip t io n

Position

World-space position of the sound

Volume

Pitch

Volume multiplier (default 1.0 )

Pitch multiplier (default 1.0 , 2.0 = one octave up)

Distance

Max audible distance in units (default 15 000)

SpacialBlend

0 = fully 2D, 1 = fully 3D (default 1.0 )

Occlusion

IsPlaying

Paused

Time

Whether geometry can block the sound (default true )

true while the sound is still active

Pause or resume without stopping

Playback position in seconds (seekable)

D e s c r ip t io n

TargetMixer

Route to a specific audio mixer

St opping a sound

// Instant stop
_engineLoop.Stop();

// Fade out over 1.5 seconds
_engineLoop.Stop( 1.5f );

After Stop() the handle becomes invalid. Accessing properties on an invalid handle is safe - they simply

do nothing.

St op everyt hing

Sound.StopAll( fade: 0.5f );

GameObject.PlaySound

GameObject.PlaySound plays a sound that f ollows the GameObject's world position every frame. This is

the recommended way to play sounds on moving objects - footsteps, projectile impacts, character voices.

// Plays the sound at this object's position and follows it
var handle = GameObject.PlaySound( FootstepSound );

// Plays the sound at around the player's head - offset is local
var handle = GameObject.PlaySound( FootstepSound, Vector3.Up * 64f );

The returned SoundHandle is just like any other - you can adjust volume, pitch, or call Stop() on it.

St oppingall sounds on a GameObject

// Stops every sound currently following this GameObject
GameObject.StopAllSounds();

// Fade out over 0.5 seconds
GameObject.StopAllSounds( fadeOutTime: 0.5f );

GameObject.PlaySound internally sets SoundHandle.Parent and SoundHandle.FollowParent =

true . You can do this manually for sounds started with Sound.Play if you need the same

behaviour:

var handle = Sound.Play( FootstepSound, WorldPosition );
handle.Parent = GameObject;
handle.FollowParent = true;

For sounds that don't need runtime code control, add one of these components to a GameObject in the

editor:

Co mp o ne nt

D e s c r ip t io n

SoundPointComponent

Plays a sound at a fixed world point. Supports auto-play, looping, and a randomised

repeat interval.

SoundBoxComponent

Like SoundPointComponent , but the source position is constrained to a box region.

SoundscapeTrigger

Blends in an ambient soundscape when the audio listener enters the trigger.

AudioListener

Overrides the listening position. Without this, audio is heard from the camera.

AudioList ener

By default the player hears sounds from the camera's position. Add an AudioListener component to a

different GameObject (e.g., the player's head bone) to move the listening point.

Create d 4 May 2026

Updated 4 May 2026