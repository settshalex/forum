# Forum project

Database structure

<pre>
create table public.posts (
  id bigint primary key not null default nextval('posts_id_seq'::regclass),
  text text not null,
  created_at timestamp without time zone not null,
  user_id bigint not null,
  foreign key (user_id) references public.users (id)
  match simple on update no action on delete no action
);

create table public.threads (
  id bigint primary key not null default nextval('threads_id_seq'::regclass),
  title character varying(1000) not null,
  created_by bigint not null,
  created_at time without time zone not null,
  foreign key (created_by) references public.users (id)
  match simple on update no action on delete no action
);

create table public.threads_posts (
  thread_id bigint not null default nextval('threads_posts_thread_id_seq'::regclass),
  post_id bigint not null,
  foreign key (post_id) references public.posts (id)
  match simple on update no action on delete no action,
  foreign key (thread_id) references public.threads (id)
  match simple on update no action on delete no action
);

create table public.users (
  id bigint primary key not null default nextval('users_id_seq'::regclass),
  email character varying(300) not null,
  password character varying(200)
);
create unique index users_id_uindex on users using btree (id);
create unique index users_email_uindex on users using btree (email);


</pre>
