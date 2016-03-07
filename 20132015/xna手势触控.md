title: XNA：手势触控
categories:
  - WP8
date: 2013-05-28 11:34:51
tags:
  - WP8
---

使用到手势触控操作时，需要引入using Microsoft.Xna.Framework.Input.Touch;
<pre>针对Page页面有三个触控：
ManipulationCompleted：结束触屏
ManipulationDulta：触屏时
ManipulationStart：触屏启动时</pre>
**TouchLocation 用来保存某一个触摸点的状态信息。**
**TouchCollection  是保存了当前所有触控状态（TouchLocation）的集合。**
当我们把一个指头在屏幕上操作，可能会有这样三种动作：按，移动，移开。那么这三个操作在WP7的XNA里如何获取呢？我们就需要了解XNA里的TouchPanel和TouchCollection这两个类
<pre>        TouchCollection touchState= TouchPanel.GetState();
        Foreach(TouchLocation location in touchState)
        {
                switch(location.State)
                {
                    case TouchLocationState.Pressed://按下
                     ……
                    break;

        case TouchLocationState.Moved://移动
                     ……
                    break;

        case TouchLocationState.Released://释放
                     ……
                    break;

        }
        }</pre>
<div>TouchLocation ：
State  触摸状态，包含4个状态
&gt; TouchLocationState.Pressed 表示屏幕被触摸时手指按下的一瞬间
&gt; TouchLocationState.Moved 表示手指按下后正在移动，经过测试可知，在手指按下的一瞬间State为Pressed ，在手指按下后抬起前这段时间内的状态均是Moved
&gt; TouchLocationState.Invalid 无效状态
&gt; TouchLocationState.Released 表示手指抬起的一瞬间
ID 表示当前触摸事件的ID，一个完成的触控事件的过程应该是“Pressed  -&gt; Moved  -&gt; Released ”在这个过程中ID是一致的，用来在多点触摸时区分触摸的每个点。
Position 触摸位置，包含两个属性
&gt; X 当前触摸位置的X轴坐标
&gt; Y 当前触摸位置的Y轴坐标
（横屏全屏情况下，屏幕的左上角坐标为（0，0）右下角坐标为（800,480））
和触控操作类似的还有叫“手势”的，也算复杂的触控吧。</div>
<div>
<pre>TouchPanel.EnabledGestures = GestureType.FreeDrag;
//用来指定手势，必须要先设定，否则报错
if (TouchPanel.EnabledGestures != GestureType.None)
{
switch (TouchPanel.ReadGesture())
{
case GestureType.Tap: //单击
break;
case GestureType.DoubleTap://双击
break;
case GestureType.FreeDrag://自由拖动
break;
case GestureType.DragComplete://拖动完成
break;
case GestureType.Flick://轻弹
break;
case GestureType.Hold://按住不动
break;
case GestureType.HorizontalDrag://横向拖动
break;
case GestureType.None://无手势
break;
case GestureType.Pinch://捏
break;
case GestureType.PinchComplete://捏完
break;
case GestureType.VerticalDrag://纵向拖动
break;
}
}</pre>
</div>
示例一各种手势的测试：
<pre>using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Audio;
using Microsoft.Xna.Framework.Content;
using Microsoft.Xna.Framework.GamerServices;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
using Microsoft.Xna.Framework.Input.Touch;
using Microsoft.Xna.Framework.Media;

namespace Gestures
{
    /// &lt;summary&gt;
    /// This is the main type for your game
    /// &lt;/summary&gt;
    public class Game1 : Microsoft.Xna.Framework.Game
    {
        GraphicsDeviceManager graphics;
        SpriteBatch spriteBatch;

        SpriteFont spriteFont;

        String message = "Do something";
        Vector2 messagePos = Vector2.Zero;
        Color color = Color.Black;

        public Game1()
        {
            graphics = new GraphicsDeviceManager(this);
            Content.RootDirectory = "Content";

            // Frame rate is 30 fps by default for Windows Phone.
            TargetElapsedTime = TimeSpan.FromTicks(333333);
        }

        /// &lt;summary&gt;
        /// Allows the game to perform any initialization it needs to before starting to run.
        /// This is where it can query for any required services and load any non-graphic
        /// related content.  Calling base.Initialize will enumerate through any components
        /// and initialize them as well.
        /// &lt;/summary&gt;
        protected override void Initialize()
        {
            //添加各种手势的支持
            TouchPanel.EnabledGestures = GestureType.Tap 
  | GestureType.DoubleTap | GestureType.Hold
  | GestureType.HorizontalDrag
  | GestureType.VerticalDrag | GestureType.FreeDrag 
  | GestureType.DragComplete | GestureType.Pinch
  | GestureType.PinchComplete | GestureType.Flick;

            base.Initialize();
        }

        /// &lt;summary&gt;
        /// LoadContent will be called once per game and is the place to load
        /// all of your content.
        /// &lt;/summary&gt;
        protected override void LoadContent()
        {
            // Create a new SpriteBatch, which can be used to draw textures.
            spriteBatch = new SpriteBatch(GraphicsDevice);

            //记载字体资源
            spriteFont = Content.Load&lt;SpriteFont&gt;("SpriteFont1");
        }

        /// &lt;summary&gt;
        /// UnloadContent will be called once per game and is the place to unload
        /// all content.
        /// &lt;/summary&gt;
        protected override void UnloadContent()
        {
            // TODO: Unload any non ContentManager content here
        }

        /// &lt;summary&gt;
        /// Allows the game to run logic such as updating the world,
        /// checking for collisions, gathering input, and playing audio.
        /// &lt;/summary&gt;
        /// &lt;param name="gameTime"&gt;Provides a snapshot of timing values.&lt;/param&gt;
        protected override void Update(GameTime gameTime)
        {
            // Allows the game to exit
      if (GamePad.GetState(PlayerIndex.One).Buttons.Back ==
         ButtonState.Pressed)
                this.Exit();

            //判断手势的类别
            if (TouchPanel.IsGestureAvailable)
            {
                GestureSample gesture = TouchPanel.ReadGesture();
                switch (gesture.GestureType)
                {
                    case GestureType.Tap:
                        message = "That was a Tap";
                        color = Color.Red;
                        break;

                    case GestureType.DoubleTap:
                        message = "That was a Double Tap";
                        color = Color.Orange;
                        break;

                    case GestureType.Hold:
                        message = "That was a Hold";
                        color = Color.Yellow;
                        break;

                    case GestureType.HorizontalDrag:
                        message = "That was a Horizontal Drag";
                        color = Color.Blue;
                        break;

                    case GestureType.VerticalDrag:
                        message = "That was a Vertical Drag";
                        color = Color.Indigo;
                        break;

                    case GestureType.FreeDrag:
                        message = "That was a Free Drag";
                        color = Color.Green;
                        break;

                    case GestureType.DragComplete:
                        message = "Drag gesture complete";
                        color = Color.Gold;
                        break;

                    case GestureType.Flick:
                        message = "That was a Flick";
                        color = Color.Violet;
                        break;

                    case GestureType.Pinch:
                        message = "That was a Pinch";
                        color = Color.Violet;
                        break;

                    case GestureType.PinchComplete:
                        message = "Pinch gesture complete";
                        color = Color.Silver;
                        break;
                }

                messagePos = gesture.Position;
            }

            base.Update(gameTime);
        }

        /// &lt;summary&gt;
        /// This is called when the game should draw itself.
        /// &lt;/summary&gt;
        /// &lt;param name="gameTime"&gt;Provides a snapshot of timing values.&lt;/param&gt;
        protected override void Draw(GameTime gameTime)
        {
            GraphicsDevice.Clear(Color.CornflowerBlue);

            //绘制屏幕的文字
            spriteBatch.Begin();
            spriteBatch.DrawString(spriteFont, message, messagePos, color);
            spriteBatch.End();

            base.Draw(gameTime);
        }
    }
}</pre>
示例二多点触控的测试：
<pre>RootDirectory = "Content";

            // Frame rate is 30 fps by default for Windows Phone.
            TargetElapsedTime = TimeSpan.FromTicks(333333);
        }

        /// &lt;summary&gt;
        /// Allows the game to perform any initialization it needs to before starting to run.
        /// This is where it can query for any required services and load any non-graphic
        /// related content.  Calling base.Initialize will enumerate through any components
        /// and initialize them as well.
        /// &lt;/summary&gt;
        protected override void Initialize()
        {
            // TODO: Add your initialization logic here

            base.Initialize();
        }

        /// &lt;summary&gt;
        /// LoadContent will be called once per game and is the place to load
        /// all of your content.
        /// &lt;/summary&gt;
        protected override void LoadContent()
        {
            // Create a new SpriteBatch, which can be used to draw textures.
            spriteBatch = new SpriteBatch(GraphicsDevice);

            // TODO: use this.Content to load your game content here
            spriteFont = Content.Load&lt;SpriteFont&gt;("SpriteFont1");
        }

        /// &lt;summary&gt;
        /// UnloadContent will be called once per game and is the place to unload
        /// all content.
        /// &lt;/summary&gt;
        protected override void UnloadContent()
        {
            // TODO: Unload any non ContentManager content here
        }

        /// &lt;summary&gt;
        /// Allows the game to run logic such as updating the world,
        /// checking for collisions, gathering input, and playing audio.
        /// &lt;/summary&gt;
        /// &lt;param name="gameTime"&gt;Provides a snapshot of timing values.&lt;/param&gt;
        protected override void Update(GameTime gameTime)
        {
            // Allows the game to exit
            if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed)
                this.Exit();

            // TODO: Add your update logic here
            touchCollection = TouchPanel.GetState();

            base.Update(gameTime);
        }

        /// &lt;summary&gt;
        /// This is called when the game should draw itself.
        /// &lt;/summary&gt;
        /// &lt;param name="gameTime"&gt;Provides a snapshot of timing values.&lt;/param&gt;
        protected override void Draw(GameTime gameTime)
        {
            GraphicsDevice.Clear(Color.CornflowerBlue);

            // TODO: Add your drawing code here
            spriteBatch.Begin();

            foreach (TouchLocation touch in touchCollection)
                spriteBatch.DrawString(spriteFont, "ID: " + touch.Id.ToString() + " (" +
                    (int)touch.Position.X + "," + (int)touch.Position.Y + ")", touch.Position, Color.White);

            spriteBatch.End();

            base.Draw(gameTime);
        }
    }
}</pre>