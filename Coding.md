Code
====

Coding for school





Code - 


using System;
using System.Collections.Generic;
using System.Linq;
using System;
using wServer.logic.attack;
using wServer.logic.loot;
using wServer.logic.movement;
using wServer.logic.taunt;
using System.Text;
using wServer.logic.cond;

namespace wServer.logic
{
    partial class BehaviorDb
    {
        private static _ Bella = Behav()
                    .Init(0x7410, Behaves("vlntns Loot Balloon Bella",
                    new RunBehaviors(
                        Once.Instance(SetConditionEffect.Instance(ConditionEffectIndex.Invulnerable)),
                        Once.Instance(new SetKey(-1,0)),

                    IfEqual.Instance(-1,0,
                     new QueuedBehavior(
                         CooldownExact.Instance(2500),
                         UnsetConditionEffect.Instance(ConditionEffectIndex.Invulnerable),
                         new SetKey(-1,1)
                        ))
                         ),
                        loot: new LootBehavior(LootDef.Empty,
                            Tuple.Create(100, new LootDef(0, 3, 1, 2,
                            Tuple.Create(0.01, (ILoot)new ItemLoot("Diamond Bladed Katana")),
                            Tuple.Create(0.01, (ILoot)new ItemLoot("Staff of Adoration")),
                            Tuple.Create(0.01, (ILoot)new ItemLoot("Wand of Budding Romance")),
                            Tuple.Create(0.01, (ILoot)new ItemLoot("Heartfind Dagger")),
                            Tuple.Create(0.01, (ILoot)new ItemLoot("Vinesword")),
                            Tuple.Create(0.01, (ILoot)new ItemLoot("Cupid's Bow"))
                            ))
                        )
                    )



                              


         )
                    .Init(0x738c, Behaves("vlntns Botany Bella",
	new RunBehaviors(
                   HpLesser.Instance(10000, new SetKey(-1,4)),
                   Once.Instance(new SetKey(-1,0)),
                   IfEqual.Instance(-1,0,
                   new RunBehaviors(
                 	SmoothWandering.Instance(2f, 2f),
                    Cooldown.Instance(750, PredictiveMultiAttack.Instance(25, 45 * (float)Math.PI / 180, 4, 0)),
                    Cooldown.Instance(950, PredictiveMultiAttack.Instance(25, 60 * (float)Math.PI / 180, 4, 0, 3)),
                    HpLesser.Instance(75000, new SetKey(-1,1)))),
                   IfEqual.Instance(-1,1,
                   new RunBehaviors(
                 	SmoothWandering.Instance(2f, 2f),
                 	Cooldown.Instance(2000, RingAttack.Instance(12, 0, 0, projectileIndex: 1)),
                    HpLesser.Instance(65000, new SetKey(-1,2)))),
                   IfEqual.Instance(-1,2,
                   new RunBehaviors(
                 	Cooldown.Instance(2000, RingAttack.Instance(12, 0, 0, projectileIndex: 0)),
                 	InfiniteSpiralAttack.Instance(200, 6, 7, projectileIndex:2),
                 	HpLesser.Instance(55000, new SetKey(-1,3)))),
                   IfEqual.Instance(-1,3,
                   new RunBehaviors(
					InfiniteSpiralAttack.Instance(501, 5, -7.5f, projectileIndex: 1),
                     InfiniteSpiralAttack.Instance(501, 5, 7.5f, projectileIndex: 1),
                     Once.Instance(SpawnMinionImmediate.Instance(0x739a,2,5,5)))),
                   IfEqual.Instance(-1,4,
                       new QueuedBehavior(
                           SetConditionEffect.Instance(ConditionEffectIndex.Invincible),
                           new SimpleTaunt("YOU WILL NOT LEAVE HERE ALIVE!"),
                           CooldownExact.Instance(5000),
                           SpawnMinionImmediate.Instance(0x7410,1,1,1),
                           Cooldown.Instance(1),
                           Die.Instance
                          ))
                  )))
                    .Init(0x739a, Behaves("vlntns Bella Buds",
	new RunBehaviors(
Once.Instance(SetConditionEffect.Instance(ConditionEffectIndex.Invulnerable)),
                               Chasing.Instance(3, 11, 1, null),
Cooldown.Instance(1000, RingAttack.Instance(3, 0, 0, projectileIndex: 0)),
                If.Instance(EntityLesserThan.Instance(30, 1, 0x738c),
                                       Die.Instance
                                      ))));

        	                      	
            }
}
