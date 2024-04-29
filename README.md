void	camera_dir_set(t_game *game)
{
	if (game->player == 'E')
	{
		game->data.dir_x = 0;
		game->data.dir_y = 1;
		game->data.plane_x = 0.66;
		game->data.plane_y = 0;
	}
	if (game->player == 'W')
	{
		game->data.dir_x = 0;
		game->data.dir_y = -1;
		game->data.plane_x = -0.66;
		game->data.plane_y = 0;
	}
}

void	camera_dir_set2(t_game *game)
{
	if (game->player == 'N')
	{
		game->data.dir_x = -1;
		game->data.dir_y = 0;
		game->data.plane_x = 0;
		game->data.plane_y = 0.66;
	}
	if (game->player == 'S')
	{
		game->data.dir_x = 1;
		game->data.dir_y = 0;
		game->data.plane_x = 0;
		game->data.plane_y = -0.66;
	}
}

void	data_init(t_game *game)
{
	game->data.mlx = mlx_init();
	game->data.pos_x = game->y_player + 0.5;
	game->data.pos_y = game->x_player + 0.5;
	camera_dir_set(game);
	camera_dir_set2(game);
	game->data.up = 0;
	game->data.down = 0;
	game->data.left = 0;
	game->data.right = 0;
	game->data.l_strafe = 0;
	game->data.r_strafe = 0;
}
